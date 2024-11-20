+++
date = '2024-11-20'
title = 'How To Config Instant-ngp'
author = 'Saka'
description = "Recording my Instant-ngp Learning"
categories = [
    "AIGC"
]
tags = [
    "Instant-ngp",
    "Tutorial",
    "Machine Learning"
]
+++

**all of operations below are just tested in Ubuntu Env of my Personal Computer**

### 1. Install Nvidia Driver && Anaconda

```shell
nvidia-smi  # check GPU-Driver version
```

check my Tips of Config Envs in Linux to config anaconda  

### 2. Check which version cuda your computer support && Install
[Nvidia Official Document](https://docs.nvidia.com/cuda/cuda-toolkit-release-notes/index.html)

[CUDA all history Version](https://developer.nvidia.com/cuda-toolkit-archive)

finally add path to your bash file:
```shell
export PATH=/usr/local/cuda-12.2/bin:$PATH
```

### 3. Install OpenGL
```Shell
sudo apt install libgl-dev
sudo apt install libglfw3-dev
```
then use official github page way to install







