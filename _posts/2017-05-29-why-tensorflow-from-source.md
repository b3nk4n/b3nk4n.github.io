---
title: Why should I install TensorFlow from Source?
author:
  name: Benjamin Sautermeister
categories: [Machine Learning]
tags: [tensorflow, performance]
pin: false
---

There are various ways to install TensorFlow. For instance, you can install it using a Docker image
or Python's package manager pip. But since the version 1.0 release of TensorFlow, you probably might have faced the following
warnings each time you run a TensorFlow session:

```console
2017-05-29 11:50:22.977500: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use SSE4.1 instructions, but these are available on your machine and could speed up CPU computations.
2017-05-29 11:50:22.977513: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use SSE4.2 instructions, but these are available on your machine and could speed up CPU computations.
2017-05-29 11:50:22.977517: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use AVX instructions, but these are available on your machine and could speed up CPU computations.
2017-05-29 11:50:22.977519: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use AVX2 instructions, but these are available on your machine and could speed up CPU computations.
2017-05-29 11:50:22.977521: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use FMA instructions, but these are available on your machine and could speed up CPU computations.
```

Of course, these are just warnings you could simply ignore, or even deactivate using the following shell command:

```console
$ export TF_CPP_MIN_LOG_LEVEL=2
```

But this just hiding and not actually solving the problem. What are these warnings about? At least the TensorFlow pip packages
r1.0, r1.1 and r1.2 are compiled with no support for latest instruction sets (SSE 4.1, SSE 4.2, AVX, AVX2, FMA) of newer CPUs,
such as Skylake or Kaby Lake. The reason might be that users of older CPUs are able to install and use these packages without
any problems as well. But in order to take advantage of these newer instruction sets, it is currently required to install
TensorFlow from source.

## Installation

The installation process is actually simple to follow and described on the TensorFlow webpage. To install the (currently) latest
release 1.2 from Source, check out this
[Install TensorFlow from Sources](https://www.tensorflow.org/versions/r1.2/install/install_sources) guide.
I'm not completely sure, but I think that prior r1.2, it was requried to activate these instructions one by one:

```console
$ sudo bazel build --config opt --copt=-msse4.1 --copt=-msse4.2 --copt=-mavx --copt=-mavx2 \
                   --copt=-mfma //tensorflow/tools/pip_package:build_pip_package
```

But in r1.2, these copt options have been renamed. For example, -mfma has been renamed to -mnofma. Consequently, it looks like
that these instructions are now enabled by default when we install TensorFlow from source. Hence, we can simple use the default
configuration and simply combile it using Bazel without any additional options:

```console
$ bazel build --config=opt //tensorflow/tools/pip_package:build_pip_package
```

> The command above is about the CPU only setup. The GPU enabled setup is different.
{: .prompt-info }

This took almost 39 minutes on my Lenovo T470 (7200U, 16GB RAM, 512GB NVMe SSD) machine, so grab a coffee!
And don't worry regarding all these compiler warnings. You will definitely see lots of them.

After the compilation, you can create and install the pip package:

```console
$ bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg
$ sudo pip install /tmp/tensorflow_pkg/tensorflow-1.2.0rc1-cp27-cp27mu-linux_x86_64.whl
```

Please keep in mind that the file name of the used `/tmp/tensorflow_pkg/tensorflow-1.2.0rc1-cp27-cp27mu-linux_x86_64.whl`{: .filepath }
file could be different depending of the configuration you have chosen. So simply check out the generated file in the
`/tmp/tensorflow_pkg`{: .filepath } folder.

## The verdict

In case you are using the *CPU only* version, it is definitely worth to compile it from source. I checked it out on a simple
example and the performance feels to be about 1.5 to 2 times better. But depending on the problem, you might even see a speed up
of factor 4 to 8. Especially large matrix multiplications, like in fully-connected layers with a lot of neurons, 
can benefit a lot from these newer instructions. Now, you might think that you do not need to compile from source in case you are
using the GPU enabled version of TensorFlow. But I would recommend to compile from source nevertheless. 
The reason is that in case you are using a input pipeline with a lot of preprocessing, you will definitely see a performance
difference as well. At least it is recommended to assign all ops to the CPU that are related to the input pipeline, 
using the `with tf.device('/cpu:0')` statement.