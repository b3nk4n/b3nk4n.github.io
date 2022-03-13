---
title: Python + Matplotlib = Must Have on Your System
author:
  name: Benjamin Sautermeister
categories: [Software Engineering]
tags: [python, matplotlib, visualization]
pin: false
toc: false
---

In the last few weeks, I had to visualize some data from time to time. And for me, it turned out that the Python library
[Matplotlib](https://matplotlib.org/) is one of the best tools to do some quick plots. I cannot imagine that I have never
installed Python on the Windows partition of my laptop, but only on my Linux partition. And I can really recommend to have
Python and Matplotlib installed on every device, so that you have these tools at hand whenever you need to visualize some data.
In this short post, I would like to write down the few simple steps you should do.

### Getting started

If not available already, please install Python. There are many ways to do it, such as from the
official [Python Software Foundation](https://www.python.org/downloads/), or via your package manager on Ubuntu:

```console
$ sudo apt-get update
$ sudo apt-get install python
```

Next, install Matplotlib using `pip` package manager:

```console
$ pip install matplotlib
```

Then run a Python terminal, import `matplotlib.pyplot` and make plot with just a few lines of code:

```python
import matplotlib.pyplot as plt

plt.plot([8,4,2,1,0,1,2,4,8])
plt.show()
```

You will then see the results in an interactive window:

![Matplotlib example](/assets/images/posts/2017/matplotlib.png){: .shadow }
_Example plot with Matplotlib_

You can also perform multiple `plt.plot()` calls before showing the graphics, in order to stack multiple lines in a
single diagram. And of course, the library allows you to do much more. To get started, check out this
[tutorial](http://matplotlib.org/users/pyplot_tutorial.html).
