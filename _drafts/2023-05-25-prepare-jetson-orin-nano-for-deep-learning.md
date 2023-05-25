---
layout: post
title:  Prepare Jetson Orin Nano for Deep Learning
date:   2023-05-25
description: Install PyTorch, OpenCV on Jetson Orin Nano
tags: [Jetson]
# categories: Jetson
---

While I was excited to get the new Jetson Orin Nano for my project, I had to face (literally) numerous number of issues and had some hard time solving them. 
I feel the need to document step-by-step configuration for (mostly) myself and maybe for some future users who might stumble upon my blog while searching for a fix

## Useful links
- [Getting Started Nvidia official guide](https://developer.nvidia.com/embedded/learn/get-started-jetson-orin-nano-devkit)
- [Jetson Orin Nano official forum](https://forums.developer.nvidia.com/c/agx-autonomous-machines/jetson-embedded-systems/jetson-orin-nano/632)

## Install PyTorch

## Install OpenCV natively
For vision related projects, you might need to install OpenCV natively on your Orin for CUDA and other frameworks support. I found the repo from [Qengineering](https://github.com/Qengineering/Install-OpenCV-Jetson-Nano) very useful. I just needed to change a few line of codes for it to work on the Orin. If you are using the original Jetson nano, Qengineering has all the resources you need to do whatever.

{% include repository/repo.html repository='Qengineering/Install-OpenCV-Jetson-Nano' %}

### Download the installation script for OpenCV 4.7.0
```shell
wget https://github.com/Qengineering/Install-OpenCV-Jetson-Nano/raw/main/OpenCV-4-7-0.sh
```

```shell
...
sudo apt-get install -y libgtk2.0-dev libgtk-3-dev libcanberra-gtk*
sudo apt-get install -y python-dev python-numpy python-pip # line 17: Delete
sudo apt-get install -y python3-dev python3-numpy python3-pip
...
-D WITH_CUDA=ON \
-D CUDA_ARCH_BIN=8.7 \ # Line 59: 5.3 -> 8.7
-D CUDA_ARCH_PTX="" \
...
-D INSTALL_PYTHON_EXAMPLES=OFF \
-D PYTHON3_PACKAGES_PATH=/usr/lib/python3/dist-packages \ # Line 81: Check Python Path
-D OPENCV_GENERATE_PKGCONFIG=ON \
...
```

I changed and checked the three lines mentioned above. Please read the script line by line and change any settings to match your needs. 

### Swap Memory for faster installation
With the memory alone, the installation can take up to 3.5 hours. However if memory swap is enabled and have access to more than 8.5GB of memory, you can decrease the installation time a little.