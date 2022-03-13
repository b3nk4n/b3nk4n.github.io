---
title: How to Setup an eGPU on Ubuntu for TensorFlow
author:
  name: Benjamin Sautermeister
categories: [Machine Learning]
tags: [tensorflow, egpu, performance, linux]
pin: false
---

I remember when I read about eGPUs for the first time. The symbiosis of having a light weight laptop at university or on the go,
 but still having a desktop like power horse when having some spare-time at home sounded like a dream. 
 But everything faded into obscurity because I almost lost full interest into gaming the last years.

But this changed, since I'm spending a lot of time in deep learning since about two years. And it's well known that taking
advantage of a GPU boosts training time by a huge margin. That's why I tried to get access to a high-performance
graphics card in order to be able to train non-trivial networks and so some more serious research.

At first, I had a look at some offers in the cloud. I did not try out a GPU-enabled instance on AWS, 
because the use a billing based on a hourly rate. This means that you have to pay for a full hour, 
even when you just run a simple example for 1 minute. Next, I checkout out the 300$ free credit on Google compute engine.
Unfortunately, the offer was limited to a 8-core CPU instance, while no GPU instance was available. Last but not least,
I checked out [FloydHub](https://www.floydhub.com/), which actually worked quite well. 
The free version comes with 10 hours of GPU access on a [Nvidia Tesla K80](https://www.nvidia.com/en-us/data-center/tesla-k80/).
However, this is a dual-GPU and you only get access to one of them, so the performance is actually worse than it looks like
on most benchmarks.

After checking out some of these cloud platforms, I was still curious about how an eGPU performs with TensorFlow. 
There was basically no benchmark available regarding eGPU setups for Machine Learning. 
Most or even all of them are focused on pure gaming. And that's why I thought: well, then do it yourself!

Of course, there were two big bullet points which made me hesitate some more days:
- High GPU prices due to crypto-currency mining
- No official support and only very few resources for most eGPU systems on Linux

**TL;DR** Yes, it is worth it!

## Installation

While the setup of the eGPU on Windows is literally plug & play, there is much more to do on Ubuntu 17.10.
In this post, I wanted to share how I achieved to run a simple TensorFlow r1.6 example on the eGPU. 
The test-system in my case was the ThinkPad X1 Carbon 6th Gen.

### 1. UEFI/BIOS security settings

On my system, I had to disable some security features in the UEFI/BIOS settings. I had to disable the following,
otherwise my eGPU was not detected:
- Secure Boot
- Thunderbolt Security Level

### 2. Install NVIDIA graphics driver

Next, the graphics drivers have to be installed. These available driver versions for linux can be found on
[launchpad](https://launchpad.net/~graphics-drivers/+archive/ubuntu/ppa). Interestingly, I installed the
latest version 390 first, but after installing CUDA, the version 387.34 has been installed out of the sudden. 
I'm not sure whether CUDA is bundled with an appropriate graphics driver, but at least the version number changed
after the installation. Nevertheless, I performed the following commands.

Optionally, uninstall old drivers first:
```console
$ sudo apt-get purge nvidia*
```

Then get and install the drivers:
```console
$ sudo add-apt-repository ppa:graphics-drivers
$ sudo apt-get update
$ sudo apt-get install nvidia-390
```

Replace the 390 with the version you would like to install. To verify the driver installation, you can use the following command:

```console
$ lsmod | grep nvidia
```

The output should be non-empty in case of success. A restart after the driver installation might be required.

To be able to use the `nvidia-smi` command, I added the following lines to my `~/.bashrc`{: .filepath } script:

```bash
# NVIDIA driver and tools
export PATH="$PATH:/usr/lib/nvidia-390:/usr/lib/nvidia-390/bin"
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/lib/nvidia-390:/usr/local/lib"
```

Again, replace the version number with the version you installed previously.

The NVIDIA system management interface might still fail with an error. This is because you have to manually switch to
your dedicated GPU first. This can be done using the following command:

```console
$ sudo prime-select nvidia
```

As far as I know, this is kind of the Linux counterpart to [NVIDIA Optimus](https://en.wikipedia.org/wiki/Nvidia_Optimus)
on Windows. Enter the nvidia-smi command again, and you should get the anticipated output.

```console
$ nvidia-smi
Tue Apr  4 23:33:18 2018       
+-----------------------------------------------------------------------------+                       
| NVIDIA-SMI 387.34               Driver Version: 387.34                      |                       
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap| Memory Usage         | GPU Util. Compute M. |
|===============================+======================+======================|
|   0  GeForce GTX 107...  Off  | 00000000:3E:00.0 Off |                  N/A |
|  0%  26C     P0    35W / 180W |       0MiB / 8114MiB |      4%      Default |
+-----------------------------------------------------------------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU  PID     Process name                                       Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+
```

> Please remember that the `prime-select` command has to be executed every time you reboot your system
and reconnect your eGPU via Thunderbolt 3.
{: .prompt-info }



### 3. Setup TensorFlow with GPU support

The installation requirements for TensorFlow with GPU support can be found on the 
[TensorFlow website](https://www.tensorflow.org/install/install_linux#nvidia_requirements_to_run_tensorflow_with_gpu_support). 
However, I found the installation is still a bit tricky, especially because it is important to install the exact CUDA
and cuDNN versions. That's why I want to share the commands and links I have used nevertheless. In my case,
I installed TensorFlow r1.6 via pip, which requires CUDA 9.0 and cuDNN 7.0. In my first try, I installed CUDA 9.1 and cuDNN 7.1,
and it did not work. Importing TensorFlow in Python resulted therefore with a warning that the appropriate libraries
could not be found.

#### 3.1 Download and install CUDA 9.0

CUDA version 9.0 can be found on the [Nvidia Developer website](https://developer.nvidia.com/cuda-90-download-archive), 
while the latest version is available in the [CUDA downloads](https://developer.nvidia.com/cuda-downloads).
I installed the main binary first, then followed by both batches. To install the binary, I used the following commands:

```console
$ sudo dpkg -i cuda-repo-ubuntu1704-9-0-local_9.0.176-1_amd64.deb
$ sudo apt-key add /var/cuda-repo-9-0-local/7fa2af80.pub
$ sudo apt-get update
$ sudo apt-get install cuda
```

Furthermore, add something like this e.g. to your `~/.bashrc`{: .filepath } script:

```bash
# NVIDIA CUDA
export PATH="$PATH:/usr/local/cuda/bin"
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/cuda/lib64"
```

#### 3.2 Download and install cuDNN 7.0

Navigate to the [cuDNN page](https://developer.nvidia.com/cudnn), register, and download the appropriate cuDNN version.
In my case, I installed version 7.0.5, which was the latest version of the 7.0 release. Afterwards,
you should set the `CUDA_HOME` environment variable, such as in your .bashrc script:

```bash
# NVIDIA cuDNN
export CUDA_HOME="/usr/local/cuda"
```

#### 3.3 Install GPU-enabled TensorFlow

I usually recommend to use a virtual environment for every project:

```console
$ sudo apt-get install python3-pip python3-dev python-virtualenv
$ virtualenv -p python3 gpu-env
$ source gpu-env/bin/activate
(gpu-env) $ pip install tensorflow-gpu==1.6
(gpu-env) $ python
>>> import tensorflow as tf
>>> sess = tf.InteractiveSession()

2018-04-04 01:11:50.496859: I tensorflow/core/platform/cpu_feature_guard.cc:140] Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX2 FMA
2018-04-04 01:11:51.911926: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:898] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2018-04-04 01:11:51.912711: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1212] Found device 0 with properties: 
name: GeForce GTX 1070 Ti major: 6 minor: 1 memoryClockRate(GHz): 1.683
pciBusID: 0000:3e:00.0
totalMemory: 7.92GiB freeMemory: 7.81GiB
2018-04-04 01:11:51.912725: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1312] Adding visible gpu devices: 0
2018-04-04 01:11:52.376920: I tensorflow/core/common_runtime/gpu/gpu_device.cc:993] Creating TensorFlow device (/job:localhost/replica:0/task:0/device:GPU:0 with 7543 MB memory) -> physical GPU (device: 0, name: GeForce GTX 1070 Ti, pci bus id: 0000:3e:00.0, compute capability: 6.1)

>>>
```

Hell yeah, we are finally ready to rumble!
