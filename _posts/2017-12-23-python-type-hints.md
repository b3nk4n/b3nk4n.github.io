---
title: Better IDE Support for Python with Type Hints
author: bsautermeister
categories: [Software Engineering]
tags: [python, typing]
pin: false
toc: false
---

About 12 years ago, I started to learn programming with Java and C#. Both languages are type-safe and have therefore a great
support when using an IDE like Eclipse, IntelliJ or Visual Studio. But throughout my software development journey,
I also made my hands dirty with other dynamically typed languages like JavaScript or Python.
While checking out Angular2 more than a year ago, I used [TypeScript](https://www.typescriptlang.org/) for my first time,
because it was recommended by the Angular team. I quickly realized how much painless it was to develop a web application
with TypeScript instead of using classic JavaScript. The ability to strictly assigning a data type to a variable allows
any IDE to offer much better tooling support, such as IntelliSense. At least in my point of view, programming in TypeScript
felt much more like programming in C# than in JavaScript, where I always felt like I had to know every possible function name
by heart. Which was especially difficult when you use JavaScript on a very non-regular basis.

Since I changed my focus from mobile software development more and more to machine learning, Python is now becoming more and more
my daily bread and butter. Unfortunately, I felt like facing the same dilemma. Again, Python is a dynamically typed language
and the tooling support sometimes feels horrible, even when using a great IDE like PyCharm. As an example,
check out the following function:

```python
def print_array(var, data):
    print('Variable {} shape: {}'.format(var, data.shape))
```

This function signature is hard to read. What is var and which type does it have? Is data a list, tuple or a numpy array?
Usually, we would have to read the docs or even read the underlying code to get a better idea about this function.
But doing so takes a lot of time. 

But there is a solution! Thanks to [PEP 484](https://www.python.org/dev/peps/pep-0484/), it is possible to assign a type
to a functions parameter or return value:

```python
import numpy as np

def print_array(var: str, data: np.ndarray) -> None:
    print('Variable {} shape: {}'.format(var, data.shape))

print_array('array', np.ones((4, 2)))
```

Take a look at the signature of the `print_array(...)` function. Now it is much more clear how to use this function.
And also an IDE is now able to provide better tooling support. In case the function requires a data structure such as list,
tuple or dictionary as its parameters, the `typing` module enables to solve this:

```python
from typing import List

def median(data: List[int]) -> float:
    length = len(data)
    sdata = sorted(data)
    if length % 2 == 0:
        return (sdata[(length - 1) // 2] + sdata[length // 2]) / 2
    else:
        return sdata[length // 2]

print(median([3, 5, 2, 1, 4,6]))
```

Needless to say, these type hints can be used in case of object orientation as well. Take a look at the following snippet:

```python
from typing import Tuple

class Person(object):
    def __init__(self, name: str, age: int):
        self.name = name
        self.age = age

    def info(self) -> str:
        return ': {}, {}'.format(self.name, self.age)

def create_person() -> Tuple[int, Person]:
    id = 42
    p = Person('Alice', 32)
    return id, p

id, person = create_person()
print(person.info())
```

To sum up, type hints help to understand and use functions in Python. Furthermore, the use of type hints improve the tooling
support of your IDE. As an example, [PyCharm](https://www.jetbrains.com/pycharm/) warns you in case you call a function with
a wrong parameter type:

![Wrong type in PyCharm](/assets/img/posts/2017/py_wrong_type.png){: .shadow }
_Type warning in PyCharm_

Moreover, there are many situations where PyCharm is suddenly able to tell you which functions any variable is able to call
or which properties are offered by an object:

![Python typing in PyCharm](/assets/img/posts/2017/py_typing.png){: .shadow }
_Python typing IDE support in PyCharm_

After playing around with these type hints, I cannot imagine anymore how I could survive without them.
At least as a fan of strictly typed languages, this Python feature is priceless.
