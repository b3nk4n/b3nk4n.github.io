---
title: Quick Data Visualization in Python
author:
  name: Benjamin Kan
categories: [Data Visualization]
tags: [python, matplotlib, plotly, termgraph, plotext, uniplot, tabulate, data, visualization]
pin: false
toc: false
---

In in [previous post](/posts/python-matlab-must-have/), I wrote about Matplotlib as a must have tool on your system to do
interactive data visualization in an instant.

Today, I worked on a playground project called [<i class="fab fa-github"></i> b3nk4n/quick-data-visualization](https://github.com/b3nk4n/quick-data-visualization)
where I started to collect and compare a few Python plotting libraries using a small set of data, such a nested
[Python list](https://docs.python.org/3/tutorial/datastructures.html#more-on-lists), a time-series in form of
a [NumPy](https://numpy.org/) array and a [Pandas](https://pandas.pydata.org/) dataframe.

At least the following plotting libraries are covered:

**UI-based**
- [matplotlib](https://pypi.org/project/matplotlib/)
- [plotly](https://pypi.org/project/plotly/)

**Text-based**
- [python-tabulate](https://pypi.org/project/tabulate/)
- [uniplot](https://pypi.org/project/uniplot/)
- [termgraph](https://pypi.org/project/termgraph/)
- [plotext](https://pypi.org/project/plotext/)

To give you an idea, the following recording should serve as an example.

![Terminalizer](/assets/img/posts/2022/quick-data-visualization.gif)
_Python quick data visualization in action_

Personally, I sill prefer Matplotlib over Plotly, mainly because it opens in a window instead of in a web browser by default.
However, Plotly's interactivity is definitly more powerful compared to Matplotlib, by offering features such as mouse-over
overlays. I really hope that some of these concepts end up in Matplotlib one day.

Regarding the text-based libraries, I really like Plotext because it almost works as a drop-in replacement for Matplotlib due
to the use of a very similar API. I'm very sure this was not by accident.