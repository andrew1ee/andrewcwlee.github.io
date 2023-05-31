---
layout: post
title:  Prepare Jetson Orin Nano for Deep Learning
date:   2023-05-30
description: Install compatible PyTorch, Torchvision, TensorRT and PyCUDA on Jetson Orin Nano
tags: [Jetson, PyTorch, TensorRT]
toc:
    sidebar: right
---

## Install PyTorch
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="/assets/img/posts/prepare-jetson-orin-nano-for-deep-learning/Pytorch_logo.jpg" title="pytorch logo" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

For a installing PyTorch on Ubuntu, mac or windows, I would head over to [https://pytorch.org](https://pytorch.org) and find the installation command of whichever version of Pytorch I want to install. Unfortunately, the version of Pytorch you can install on a Jetson device is quite limited.

#### Available versions
Go to [https://developer.download.nvidia.com/compute/redist/jp/v51/pytorch/](https://developer.download.nvidia.com/compute/redist/jp/v51/pytorch/) to find which versions are available for install on Jetpack 5.1.1.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="/assets/img/posts/prepare-jetson-orin-nano-for-deep-learning/available-pytorch-versions.png" title="available pytorch versions" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

As of May 30, 2023, `1.14.0` and `2.0.0` is available. Download the wheel file of your choice. Download the wheel file you want to install.

#### Install prerequisites
```shell
sudo apt-get update
```
```shell
sudo apt-get install autoconf bc build-essential g++-8 gcc-8 clang-8 lld-8 gettext-base gfortran-8 iputils-ping libbz2-dev libc++-dev libcgal-dev libffi-dev libfreetype6-dev libhdf5-dev libjpeg-dev liblzma-dev libncurses5-dev libncursesw5-dev libpng-dev libreadline-dev libssl-dev libsqlite3-dev libxml2-dev libxslt-dev locales moreutils openssl python-openssl rsync scons python3-pip libopenblas-dev
```

```shell
python3 -m pip install --upgrade pip 
```

Install Numpy and SciPy
```shell
python3 -m pip install aiohttp numpy=='1.19.4' scipy=='1.5.3'
```

Add PATH `LD_LIBRARY_PATH`
```shell
export "LD_LIBRARY_PATH=/usr/lib/llvm-8/lib:$LD_LIBRARY_PATH
```

```shell
python3 -m pip install --upgrade protobuf
```

#### Install PyTorch
Install the .whl file downloaded in the last step.
```shell
python3 -m pip install --no-cache /PATH/TO/torch-1.14.0a0+44dac51c.nv23.02-cp38-cp38-linux_aarch64.whl
```

<!-- #### Find compatible Torchvision
To find the compatible Torchvision version, clone the original torchvision repo.
```shell
git clone https://github.com/pytorch/vision.git
```
```shell
cd vision/;
python setup.py install
``` -->

## Install TensorRT for Python
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="/assets/img/posts/prepare-jetson-orin-nano-for-deep-learning/TensorRT.jpeg" title="pytorch logo" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
TensorRT is a deep learning inference framework with optimization and acceleration. Refer to more information at the [official website](https://developer.nvidia.com/tensorrt).

#### Installation 
If you followed the [Jetpack 5.1.1 documentation](https://docs.nvidia.com/jetson/jetpack/install-jetpack/index.html#package-management-tool), TensorRT would be ready to use. If not, here are the steps.

```shell
sudo add-apt-repository "deb https://repo.download.nvidia.com/jetson/common r35.3 main"
```
```shell
sudo apt update
sudo apt install nvidia-jetpack
```

#### Validation 

Run Python interpreter and import tensorrt
```py
>>> import tensorrt
>>> print(tensorrt.__version__)                # Print TensorRT version
>>> 8.5.2.2
>>> assert tensorrt.Builder(tensorrt.Logger()) # Check if tensorrt is working fine with CUDA
>>>                                            # If no error is returned, TensorRT is installed and works with CUDA
```

## Install PyCUDA

Let Jetson know where CUDA is located by adding PATHs

```shell
export PATH=/usr/local/cuda/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
```
Restart Terminal or enter the following command.
```shell
source ~/.bashrc
```

If PATH is added correctly, the following command should pring the version of nvcc (Nvidia CUDA Complier Driver)
```shell
nvcc --version
```

#### Prerequisite

```shell
python3 -m pip install Cython
```

#### Install PyCUDA
```shell
python3 -m pip install pycuda
```