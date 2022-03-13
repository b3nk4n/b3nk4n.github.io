---
title: TensorLight - A High-Level Framework for TensorFlow Projects
author:
  name: Benjamin Sautermeister
categories: [Software Engineering]
tags: [tensorflow, python, deep learning, framework]
pin: false
toc: false
---

In the course of the development of my Master's Thesis "Deep Learning Approaches to Predict Future Frames in Videos" at TUM,
I realized that the high flexibility of TensorFlow has its price: boilerpate code.
Many things that are needed in almost every neural network training or evaluation script have to be implemented
over and over again. To that end, I started to implement a high-level API for Google's machine intelligence library,
called [TensorLight](https://github.com/b3nk4n/tensorlight).

![TensorLight](/assets/images/posts/2016/tensorlight.png)
_TensorLight Framework logo_

TensorLight comes with four guiding principles:
- **Simplicity**: Straight-forward to use for anybody who has already worked with TensorFlow. Especially,
  no further learning is required regarding how to define a model's graph definition.
- **Compactness**: Reduce boilerplate code, while keeping the transparency and flexibility of TensorFlow.
- **Standardization**: Provide a standard way in respect to the implementation of models and datasets in order to save time.
  Further, it automates the whole training and validation process, but also provides hooks to maintain customizability.
- **Superiority**: Enable advanced features that are not included in the TensorFlow API, as well as retain its full functionality.

The project solution of my thesis is almost entirely based on this framework. I was able to refactor and the majority of my
training and evaluation code, as well as all the best practices I gained throughout this phase into it.
