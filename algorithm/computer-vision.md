# 计算机视觉（Computer Vision）

CodeLab 视觉方向：让机器“看懂”图像，从分类到检测、分割、视频理解。

## 常见任务

| 任务 | 做什么 | 典型模型 |
| --- | --- | --- |
| 图像分类 | 判断图片类别 | ResNet、ViT |
| 目标检测 | 定位 + 分类物体 | YOLO、RT-DETR |
| 实例/语义分割 | 像素级分类 | Mask R-CNN、SAM |
| OCR | 文字识别 | PaddleOCR |
| 视频理解 | 行为/事件识别 | 时序模型 |

## 标准管线

```text
数据采集 → 标注（LabelImg / X-AnyLabeling）→ 数据划分（train/val/test）
  → 训练（PyTorch）→ 评估（mAP/准确率）→ 推理服务（FastAPI）→ 部署
```

## 实践要点

- **数据质量 > 模型花活**：先检查标注错误、类别不均衡
- **从预训练模型开始**：别从零训练，用 ImageNet 预训练权重微调
- **固定随机种子**：结果可复现
- **划分数据集**：训练 / 验证 / 测试严格分开，测试集只评估一次
- **badcase 分析**：把错例可视化，找模式（光照、遮挡、小目标……）

## 工具栈

- PyTorch、Ultralytics（YOLO）、OpenCV
- 标注：LabelImg / X-AnyLabeling
- 训练可视化：TensorBoard / wandb
- 服务化：FastAPI + Docker（参考 [python.md](../software/python.md)）

## 常见坑

- 显存不够：降 batch size、用更小的输入尺寸、混合精度
- 过拟合：数据增强、正则化、早停
- 部署与训练环境不一致：固定依赖版本，Docker 化

## 下一步

- 工业落地：[industrial-vision.md](industrial-vision.md)
- 数据与评估规范：[overview.md](overview.md)
