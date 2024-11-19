+++
date = '2024-11-19'
title = 'Tips of Config Envs in Linux'
author = 'Saka'
description = ""
categories = [
    "Original"
]
tags = [
    "Linux",
    "Tutorial"
]

+++
## Install NodeJs via Binary Archive

first download prebuilt binaries from NodeJs official website

then unzip it to **any directory you wanna install**, remember the path [node path]

then edit `~/.zshrc` file, add below to the end

```jsx
# Nodejs
 export NODEJS_HOME=[node path]/bin
 export PATH=$NODEJS_HOME:$PATH
```

then refresh config file

`source ~/.zshrc` 

---

## install hexo

*npm install https://github.com/CodeFalling/hexo-asset-image --save*

---

## Install Anaconda

https://docs.anaconda.com/anaconda/install/linux/

**bash is necessary!!!**

---

## Install Code Env

### 1. g++/gcc

```bash
sudo apt install build-essential
```