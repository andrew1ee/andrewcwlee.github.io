---
layout: post
title:  Get Jetson Orin Nano to do some Deep Learning
date:   2023-05-30
description: Install compatible PyTorch, Torchvision and TensorRT on Jetson Orin Nano
tags: [Jetson, PyTorch, TensorRT]
toc:
    sidebar: right
---

## Install PyTorch
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="/assets/img/posts/get-jetson-nano-to-do-some-deep-learning/Pytorch_logo.jpg" title="pytorch logo" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

For a installing PyTorch on Ubuntu, mac or windows, I would head over to [https://pytorch.org](https://pytorch.org) and find the installation command of whichever version of Pytorch I want to install. Unfortunately, the version of Pytorch you can install on a Jetson device is quite limited.

#### Available versions
Go to [https://developer.download.nvidia.com/compute/redist/jp/v51/pytorch/](https://developer.download.nvidia.com/compute/redist/jp/v51/pytorch/) to find which versions are available for install on Jetpack 5.1.1.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="/assets/img/posts/get-jetson-nano-to-do-some-deep-learning/available-pytorch-versions.png" title="available pytorch versions" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

As of May 30, 2023, `1.14.0` and `2.0.0` is available. 


## Install TensorRT for Python
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="/assets/img/posts/get-jetson-nano-to-do-some-deep-learning/TensorRT.jpg" title="pytorch logo" class="img-fluid rounded z-depth-1" %}
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