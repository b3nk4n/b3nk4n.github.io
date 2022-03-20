---
title: Manage Your Java Environment
author:
  name: Benjamin Sautermeister
categories: [Software Engineering]
tags: [java]
pin: false
---

In case you are familiar with Pyhon, I guess you also have heard of [virtualenv](https://virtualenv.pypa.io/). This is a tool to create isolated
Python environments, which lets you easily create or switch projects between Python 2 and Python 3.

In Java, there are also different version out there. While version 7 or 8 are probably still most commonly used in production,
even newer versions like 10 (current default of Ubuntu 18.04) or the preview of Java 11 (release expected in late September 2018)
are available, too. Consequently, it can happen that you are working on several projects with different Java version requirements. 
The question is now: how can we switch between different installed JDKs?

There are of course multiple possible answers. Two of them are the following...

## A) Setting the default Java version

In case you have multiple Java versions installed, you can change the default version using the update-alternatives tool:

```console
$ sudo update-alternatives --config java
There are 2 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                            Priority   Status
------------------------------------------------------------
  0            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1101      auto mode
  1            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1101      manual mode
* 2            /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java   1081      manual mode

Press ENTER to keep the current choice[*], or type selection number:
```

As you can see, the command will list you all installed versions from which you can choose from.
A more detailed explanation for how to install/uninstall/configure Java on Ubuntu 18.04 can be found in this  [Linuxize article](https://linuxize.com/post/install-java-on-ubuntu-18-04/).

## B) jEnv

jEnv is a command line tool to help you forget how to set the `JAVA_HOME` environment variable.
It currently supports Linux and Mac OS X.The installation is short and described on the [jEnv website](http://www.jenv.be/). 
After installations, you can easily add JDK installations using the `jenv add /path/to/java/home` command:
Afterwards, you can either list the existing environments:

```console
$ jenv versions
  system
  oracle64-1.6.0.39
* oracle64-1.7.0.11 (set by /Users/hikage/.jenv/version)
```

Also, you can configure the used environments either globally, locally (per directory) within the shell instance:

```console
$ jenv global oracle64-1.6.0.39
$ jenv local oracle64-1.6.0.39
$ jenv shell oracle64-1.6.0.39
```

## Bonus tip: Maven Enforcer plugin

In case you manage your project with Maven in a team, I can highly recommend to use the
[Enforcer plugin](https://maven.apache.org/enforcer/maven-enforcer-plugin/). It provides goals to control certain environmental
constraints such as Maven version, JDK version or OS family along with many more built-in rules and user created rules.

As an example, we had the problem in our team that some integrations tests ran perfectly on our Jenkins, 
as well as on my colleague's machines, but not on mine in case I was running `mvn install`. 
However, these tests did not fail when running them using IntelliJ. It simply turned out that my default JDK
was suddenly set to version 10, because I recently updated my machine from Ubuntu 17.10 to 18.04. 
I was completely unaware of this to that point of time.

In case this sounds useful for you current project, then simply read the
[Usage page](https://maven.apache.org/enforcer/maven-enforcer-plugin/usage.html) of the plugin's project website.