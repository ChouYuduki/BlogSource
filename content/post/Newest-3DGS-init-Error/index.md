+++
date = '2025-07-07'
title = 'Newest 3DGS Init Error'
author = "Saka"

categories = [

    "AIGC"
]
tags = [
    "3DGaussian"
]

+++

**最新版のGaussian Splattingでのエラー：**
```
TypeError: GaussianRasterizationSettings.__new__() missing 1 required positional argument: 'antialiasing'

```
それはモデルの更新によるものです。

---
### 解決方法
このエラーを解決するには：  
`gaussian_renderer/int.py`のコードに`antialiasing=True`を増加してください：

```Python
raster_settings = GaussianRasterizationSettings(
image_height=int(data['novel_view']['height'][idx]),
image_width=int(data['novel_view']['width'][idx]),
tanfovx=tanfovx,
tanfovy=tanfovy,
bg=bg_color,
scale_modifier=1.0,
viewmatrix=data['novel_view']['world_view_transform'][idx],
projmatrix=data['novel_view']['full_proj_transform'][idx],
sh_degree=3,
campos=data['novel_view']['camera_center'][idx],
prefiltered=False,
debug=False，
**antialiasing=True**
```

出力データも修正すべき：
```Python
rendered_image, radii, _ = rasterizer(
```



