+++
date = '2024-11-27'
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

* Polynomial expansion: Uses $x^3, x^2, x^1, x^0$ to construct polynomial basis functions.
* Fourier expansion: Uses sine and cosine functions as basis functions.
* Spherical harmonic expansion: Uses $Y_l^m(θ,ϕ)$ as basis functions for the surface of a sphere.

### Hierarchical Sampling
Coarse(粗い) Network and Fine(細い) Net.
Coarse sample is uniform(一様) sampling, which cannot sapling points of edge very clearly and will lead to issues of wasted sampling points in empty spaces ineffectively. So after coarse sampling, there is a fine samling, which sample more points in rapidly changed place, like edge.

### Representing a 3D space with a continuous field
Continuous Field: This is a mathematical concept representing a mapping function where every point $(x,y,z)$ is associated with a property or value.

### Camera
The **position and orientation** of the camera are determined by its **extrinsic matrix**, while the **projection properties** are determined by its **intrinsic matrix**.

extrinsic matrix is also called w2c(world-to-camera) matrix.

---

the inverse matrix(逆行列) of w2c is c2w matrix, which is widely used in Nerf.  

the function of c2w is transform points from camera axis to world axis.

$$\begin{bmatrix} R & T\\\ 0 & 1\end{bmatrix} = \begin{bmatrix} r11 & r12 & r13 & t1 \\\ r21 & r22 & r23 & t2 \\\ r31 & r32 & r33 & t3 \\\ 0 & 0 & 0 & 1  \end{bmatrix}$$ 

---

the intrinsic matrix of camera K is below:
 

$$\begin{bmatrix}f_x & 0 & c_x\\\ 0 & f_y & c_y\\\ 0 & 0 & 1 \end{bmatrix}$$

$f_x$ and $f_y$ represent the vertical focal length and horizontal focal length

## How to Get Camera parameters

In Nerf, Intrinsic and Extrinsic parameters should be given before you start, but how can we get these parameters?

Well, there are two ways, the first way is using data from rendering software like blender.  
The second way is using real data from our own real camera.

there are some tech help us, such as COLMAP: [ColMap Link](https://colmap.github.io/), which is a sfm algorithm.

{{ <quote> }}

3DGS use colmap to initialize a point cloud

{{ </quote> }}