---
layout: post
title:  Install OpenCV natively on Jetson Orin Nano
date:   2023-05-25
description: Install OpenCV with CUDA natively on Jetson Orin Nano
tags: [Jetson]
toc:
    sidebar: right
---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="/assets/img/posts/install-opencv-on-jetson-orin-nano/jetson_orin_nano.jpg" title="opencv logo" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

While I was excited to get the new [Jetson Orin Nano](https://www.nvidia.com/en-us/autonomous-machines/embedded-systems/jetson-orin/) for my project, I ended up encountering a some number of problems that required quite a bit of effort to resolve. 
I feel the need to document step-by-step setup process primarily for my own reference, and also potentially as a resource for future users who might discover my blog while seeking solutions to similar issues.

## Useful links
- [Getting Started Nvidia official guide](https://developer.nvidia.com/embedded/learn/get-started-jetson-orin-nano-devkit)
- [Jetson Orin Nano official forum](https://forums.developer.nvidia.com/c/agx-autonomous-machines/jetson-embedded-systems/jetson-orin-nano/632)

## Install OpenCV with CUDA natively
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="/assets/img/posts/install-opencv-on-jetson-orin-nano/OpenCV_logo.png" title="opencv logo" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

For vision related projects, you might need to install OpenCV natively on your Orin for CUDA and other frameworks support. I found the repo from [Qengineering](https://github.com/Qengineering/Install-OpenCV-Jetson-Nano) very useful. I just needed to change a few line of codes for it to work on the Orin. If you are using the original Jetson nano, Qengineering has all the resources you need to do whatever.

Forked from the original repo from Q-engineering, I created a repo for Jetson Orin Nano.

{% include repository/repo.html repository='qengineering/Install-OpenCV-Jetson-Nano'%}
{% include repository/repo.html repository='andrewcwlee/Install-OpenCV-Jetson-Orin-Nano'%}

#### Download the installation script

```shell
wget https://github.com/andrewcwlee/Install-OpenCV-Jetson-Orin-Nano/raw/main/OpenCV-4-7-0.sh
```

Please open the `OpenCV-4-7-0.sh` file to custom the build for specific needs.

#### (Optional) Swap memory for faster installation
With the built-in memory alone, the installation can take up to 3.5 hours. However if memory swap is enabled and have access to more than 8.5GB of memory, you can decrease the installation time.

```shell
free -h 
df -h                            # Check free storage

# Create swap
sudo fallocate -l 8.5G /swapfile # Create swap named swapfile with 8.5GB 
ls -lh /swapfile                 # Check created swap

# Enable swap
sudo chmod 600 /swapfile         # Set permission
sudo mkswap /swapfile            # Set up the file /swapfile as swap space
sudo swapon /swapfile            # Enables the swap file immediately
free -h

# Remove swap
sudo swapoff -v /swapfile        # Disable swap
sudo rm /swapfile                # Remove swapfile
free -h
```

#### Install OpenCV
```shell
free -m
sudo chmod 755 ./OpenCV-4-7-0.sh # Set permission
./OpenCV-4-7-0.sh                # Run script
```

