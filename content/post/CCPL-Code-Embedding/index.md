+++
date = '2025-05-15'
title = 'CCPL Code Embedding'
author = "Saka"

categories = [

    "AIGC"
]
tags = [
    "3DGaussian"
]

+++
## Embedding Code
#### 1. 确认 VGG 特征输出接口
在 train_artistic.py 中，本地使用的是 scene.VGG.VGGEncoder，vgg_encoder(x) 会返回一个包含 .relu1_1、.relu2_1、.relu3_1、.relu4_1 四个属性的对象train_artistic。这些正好对应 CCPL 需要的多层特征。

#### 2. 在文件开头导入 CCPL
在 train_artistic.py 顶部（紧跟其他 import 之后）加入：

diff
Copy
Edit
 from utils.loss_utils import cal_adain_style_loss, cal_mse_content_loss
+from ccpl.net import CCPL, mlp
这里假设你已将 CCPL-main/net.py 里的 net.py 拷贝到 StyleGaussian/ccpl/net.py，并在项目根 __init__.py 中配置好 ccpl 包的导入路径。

#### 3. 在训练函数开头实例化 CCPL
找到 training(...) 函数开始部分，在创建 vgg_encoder 之后，加入：

```diff
     vgg_encoder = VGGEncoder().cuda()
+    # —— CCPL 初始化：mlp 是 net.py 中导出的 MLP 列表
+    #     num_s、num_l、tau 可从命令行参数传入
+    ccpl_fn = CCPL(mlp=mlp).cuda()
```

#### 4. 在训练主循环里计算 CCPL
找到如下位置：在渲染并计算完 content_loss 和 style_loss 之后train_artistic：

```python
        # style loss 和 content loss
        rendered_rgb_features = vgg_encoder(normalize_vgg(rendered_rgb.unsqueeze(0)))
        content_loss = cal_mse_content_loss(
            gt_image_features.relu4_1, rendered_rgb_features.relu4_1
        )
        style_loss = 0.
        for style_feature, image_feature in zip(
                style_img_features, rendered_rgb_features):
            style_loss += cal_adain_style_loss(style_feature, image_feature)

        loss = content_loss + style_loss * style_weight
```


在这里插入 CCPL 计算：
```diff
        # —— 在此处插入 CCPL
+       # 将四层特征整理为列表，注意 q 是 stylized，k 是 content
+       feats_q = [
+           rendered_rgb_features.relu1_1,
+           rendered_rgb_features.relu2_1,
+           rendered_rgb_features.relu3_1,
+           rendered_rgb_features.relu4_1,
+       ]
+       feats_k = [
+           gt_image_features.relu1_1,
+           gt_image_features.relu2_1,
+           gt_image_features.relu3_1,
+           gt_image_features.relu4_1,
+       ]
+       # start_layer/end_layer 控制 CCPL 作用的层数，比如只用 relu2~4
+       end_layer = len(feats_q)  # 4
+       start_layer = end_layer - args.num_l  # 如果 num_l=3，则 start_layer=1 (relu2)
+       ccp_loss = ccpl_fn(
+           feats_q     = feats_q,
+           feats_k     = feats_k,
+           num_s       = args.num_s,
+           start_layer = start_layer,
+           end_layer   = end_layer,
+           tau         = args.tau
+       )
+       # 将 CCPL 加权到总损失
+       loss = loss + args.ccp_weight * ccp_loss
```
#### 5. 更新命令行参数解析
在 if __name__ == "__main__": 中的 parser.add_argument(...) 部分，添加：

```diff
     parser.add_argument("--style_weight", type=float, default=10.)
     parser.add_argument("--content_preserve", action='store_true', default=False)
+    parser.add_argument("--ccp_weight", type=float, default=5.0,
+                        help="weight for Contrastive Coherence Preserving Loss")
+    parser.add_argument("--num_s", type=int, default=8,
+                        help="number of anchor samples per layer for CCPL")
+    parser.add_argument("--num_l", type=int, default=3,
+                        help="number of layers to apply CCPL (e.g., 3 means relu2_1~relu4_1)")
+    parser.add_argument("--tau", type=float, default=0.07,
+                        help="temperature for CCPL InfoNCE loss")
```

#### 6. 确认其他训练脚本无需修改
train_reconstruction.py 与 train_feature.py 仅负责重建和嵌入特征，不涉及风格迁移，不需要加 CCPL。

高层 train.py 仅调度这三个阶段，也无需修改。

总结
确认位置：只要在 train_artistic.py 的风格化训练循环里计算内容／风格损失后，立即调用 CCPL 并加权即可。

检查对齐：所用 VGG 层 .relu1_1 ~ .relu4_1 与 CCPL 多层输入完全吻合。

参数可控：通过新增的命令行参数可以方便地调节 CCPL 的强度、层数、采样数和温度。

按照上面的步骤修改并运行，相信你就能在现有的 StyleGaussian 风格化训练流程里，正确地融入 CCPL，提升多视图和视频输出的一致性与稳定性。
## Hyper-Parameter Code

#### in terminal:

```bash
python train_artistic.py \
  --source_path datasets/Furiren \
  --wikiartdir datasets/wikiart \
  --ckpt_path output/Furiren/feature/default/chkpnt/feature.pth \
  --style_weight 10 \
  
  --ccp_weight 5.0 \
  --num_s 8 \
  --num_l 3 \
  --tau 0.07 \
  --exp_name default
```

#### And here is the original terminal parameters:

```bash
python train_artistic.py \
  -s datasets/train \
  --wikiartdir datasets/wikiart \
  --ckpt_path output/train/feature/default/chkpnt/feature.pth \
  --style_weight 10

```
