---
title: Find your model's optimal hyperparameters with Hyperopt
author:
  name: Benjamin Sautermeister
categories: [Machine Learning]
tags: [hyperopt]
pin: false
toc: false
---

While checking out some tools for automated hyperparameter optimization, I came across a quite popular library called
[Hyperopt](https://hyperopt.github.io/hyperopt/). It provides an implementation for Random Search and
Tree-of-Parzen-Estimators (TPE). Unfortunately, most examples out there us a dummy function to replace the model,
but I could not find any example that uses TensorFlow. That's why I wanted to provide a basic simple Hyperopt example
with TensorFlow. This example can be found on my GitHub's
[machine-learning-examples](https://github.com/b3nk4n/machine-learning-examples/tree/master/hyperparam_opt) repository.

Do you have any experiences with other libraries for hyperparameter optimization? I would be happy if you share your experiences?
If so, I would appreciate reaching out to me. For instance, I have read that a [Sacred](http://sacred.readthedocs.io/) extension
called [Labwatch](https://github.com/automl/labwatch) also allows to define a search space for algorithmic hyperparameter
optimization, but comes with different algorithms.