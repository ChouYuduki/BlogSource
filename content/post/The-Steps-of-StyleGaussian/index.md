+++
date = '2025-05-15'
title = 'The Steps of StyleGaussian'
 
author = 'Saka'
description = "Here is some of my lab training"

categories = [

    "AIGC"
]
tags = [
    "3DGaussian"

]

+++

## How to train Your Own Models 
```bash
Step 1️⃣ train_reconstruction.py    --> 生成 point_cloud.ply
Step 2️⃣ train_feature.py           --> 提取特征
Step 3️⃣ train_artistic.py          --> 风格迁移训练

```

### 1.Get point-cloud Data

This step can be finished in Orininal Gaussian Train

![image.png](attachment:373f7f85-16b8-4da5-ae27-6abc66be918f:image.png)

Reference the Catalog of `Datasets/` dir

### 2.Reconstruct the Point Cloud

```bash
python train_reconstruction.py -s datasets/train
```

Output Model saved in: `output/train/reconstruction/`

### 3.Feature Embedding

```bash
python train_feature.py -s datasets/train \
  --ply_path output/train/reconstruction/default/point_cloud/iteration_30000/point_cloud.ply
```

Output Model saved in: `output/train/feature`

### 4.Style Transfer Training

Before this step, modify the `train_artistic.py`

and add the following code to the import part of the code:

```bash
from PIL import ImageFile
ImageFile.LOAD_TRUNCATED_IMAGES = True
```

or the broken image will stop the training.

then run the following command in terminal:

```bash
python train_artistic.py -s datasets/train \
--wikiartdir datasets/wikiart \
  --ckpt_path output/train/feature/default/chkpnt/feature.pth --style_weight 10

```

### 5.Start Viewer

```bash
python viewer.py -m output/Furiren/artistic/default \
                      --style_folder images --viewer_port 8080
```

view it in `localhost:8080`
