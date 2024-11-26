+++
date = '2024-11-25'
title = 'Nerf Source Code Explain'
author = 'Saka'
description = ""
categories = [
    "AIGC",
   
]
tags = [
    "Learning Notes",
     "Machine Learing",
     "Nerf"
]
math = true

+++

## Basic Conception

### Neual Networks
CNN, namely Convolutional(畳み込み) Neural Networks  
for example, if you want to recognize an image "X", you can change the image into matrix, then you can make three matrices
$$\begin{bmatrix}-1 & -1 & 1\\\ -1 & 1 & -1\\\ 1 & -1 & -1 \end{bmatrix}$$
$$\begin{bmatrix}1 & -1 & 1\\\ -1 & 1 & -1\\\ 1 & -1 & -1 \end{bmatrix}$$
$$\begin{bmatrix}1 & -1 & -1\\\ -1 & 1 & -1\\\ -1 & -1 & 1 \end{bmatrix}$$

which have the specific feature of "X", left-above, center, and right above. 

### Sperical harmonics

It is a type of function expansion in 3D space. It is a basis fuction on a spherical surface, similar to how Fourier series perform an orthogonal expansion on a 1D interval.

spherical harmonics can indeed be seen as a **3D basis function expansion:**

$E = mc^2$

* Polynomial expansion: Uses $x^3, x^2, x^1, x^0$ to construct polynomial basis functions.
* Fourier expansion: Uses sine and cosine functions as basis functions.
* Spherical harmonic expansion: Uses $Y_l^m(θ,ϕ)$ as basis functions for the surface of a sphere.