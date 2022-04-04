---
title: Xtext - Your Own Programming Language Here
author:
  name: Benjamin Sautermeister
categories: [Software Engineering]
tags: [xtext, dsl, eclipse, xtext, xtend, university]
pin: false
---

Did you ever dream of proposing your own programming language? If so, then [Xtext](http://www.eclipse.org/Xtext/index.html)
might be something for you.

> **LANGUAGE ENGINEERING FOR EVERYONE!**
> 
> Xtext is a framework for development of programming languages and domain-specific languages.
> With Xtext you define your language using a powerful grammar language. As a result you get a full infrastructure,
> including parser, linker, typechecker, compiler as well as editing support for Eclipse, any editor that supports
> the Language Server Protocol and your favorite web browser.
> ([source](http://www.eclipse.org/Xtext/index.html))

### Domain specific language

This [Eclipse IDE](https://www.eclipse.org/ide/) plugin enables you to use simplified
[EBNF](https://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_form) grammar to define your
[DSL](https://en.wikipedia.org/wiki/Domain-specific_language) that is just right for you. And Xtext helps you do generate
tools, parser and and editor syntax highlighting and code completion. This way it allows you to define a DSl with only
little effort. Did I get you excited? Then give the short [Xtext tutorials](http://www.eclipse.org/Xtext/documentation.html)
a try. These few minutes are well spent.

### Code generation

Furthermore, you can create a code generator to reduce boilerplate code. This is done via the integrated language
[Xtend](https://www.eclipse.org/xtend/). This language is something in between Java and C#, which however has a slightly
more compact syntax. Xtend can be used to easily generate your boilerplate code for classes, methods, properties or documentation
that usually follow a very similar strucutre.

#### Example code generator

Here is some Xtent code to get an idea how this might look like.

```
grammar org.xtext.de.htwg.ModelGen with org.eclipse.xtext.common.Terminals
generate modelGen "http://www.xtext.org/de/htwg/ModelGen"

ModelGen:
    'PACKAGE' name=QualifiedName
    'NAME' pluginName=ID
    elements+=RootElement*
;

RootElement:
    PackageDeclaration | Type | Import
;

AbstractElement:
    Type | Import
;

QualifiedName:
    ID ('.' ID)*
;

QualifiedNameWithWildcard:
    QualifiedName '.*'?
;

Type:
    Typedef | Interface
;

Typedef:
    'type' name=ID
;

PackageDeclaration:
    'package' name=QualifiedName '{'
        elements+=AbstractElement*
    '}'
;

Import:
    'import' importedNamespace = QualifiedNameWithWildcard
;

Interface:
    'interface' name=ID '{'
        methods+=Method*
    '}'
;

Method:
    'method' name=ID 
        '('(params+=Parameter 
            (',' params+=Parameter)*)?')'
        ':' type=[Type | QualifiedName]
;

Parameter:
    name=ID ':' type= [Type | QualifiedName]
;
```

Xtend then generates various artefacts such as the EMF model based on the EBNF grammar above to create our generator.
An example of our DSL could look like to following.

```
PACKAGE de.htwg.seapal.person
NAME Person

type void
type String
type boolean
type long

package model {
    interface IDatabase {
        method save(data: String): void
        method delete(id: long): boolean
        method get(id: long): String
        method close(): void
    }
}
```

The in Xtend integrated templating engine can then be used to generate your code. This enables you to generate code
in a form that is much easier to grasp compared to using a `StringBuilder` or similar. Just check out the following code snippet.

```
override void doGenerate(Resource resource, IFileSystemAccess fsa) {
    // Find root package name
    for (e: resource.allContents.toIterable.filter(typeof(Plugin))) {
        rootPackage = e.fullyQualifiedName;
        pluginName = e.name.toLowerCase().toFirstUpper();
    }

    // Generate interfaces
    for (e: resource.allContents.toIterable.filter(typeof(Interface))) {
        fsa.generateFile(
            e.fullyQualifiedName.toString("/") + ".java",
            e.compileInterface)
    }
    // …
}

def compileInterface(Interface iface)'''
    «IF iface.eContainer != null»
        package «iface.eContainer.fullyQualifiedName»;

        «FOR i:iface.eContainer.eContents.filter(typeof(Import))»
            import «rootPackage».«i.importedNamespace»;
        «ENDFOR»
    «ENDIF»

    /**
     * Generated model interface «iface.name».
     * @author TODO
     * @version TODO
     */
    public interface «iface.name» {
        «FOR m:iface.methods»
            «m.compileMethodInterface»
        «ENDFOR»
    }
'''

def compileMethodInterface(Method p) '''

    /**
     * TODO: Method description...
     * «IF p.params != null»@param TODO: describle all parameters...«ENDIF»
     * «IF !p.type.fullyQualifiedName.toString.equals("void")»@return TODO: Return value description...«ENDIF»
     */
    public «p.type.fullyQualifiedName.lastSegment» «p.name.toFirstLower»(«FOR prm:p.params SEPARATOR ", "»«prm.type.fullyQualifiedName.lastSegment» «prm.name»«ENDFOR»);
'''
```

And that's more or less it. If you now start a second Eclipse IDE instance and define a `/src-gen`{: .filepath} folder, then the code is automatically generated
depending on the textual model.