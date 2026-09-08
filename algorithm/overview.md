# 算法方向概述

CodeLab 算法部的基础规范：数据处理、模型开发、评估与交付。

## 工作内容

- 机器学习 / 深度学习建模
- 计算机视觉（见 [computer-vision.md](computer-vision.md)）
- 工业视觉（见 [industrial-vision.md](industrial-vision.md)）
- 数据清洗、特征工程、模型评估

## 标准流程

```text
问题定义 → 数据获取 → 数据探索(EDA) → 数据清洗/标注
  → 建模（baseline → 迭代） → 评估（指标+badcase）
  → 部署（FastAPI + Docker）→ 文档与成果归档
```

## 工程规范

- Python 3.12 + uv + ruff + pytest（见 [python.md](../software/python.md)）
- 代码仓库化：训练脚本、数据管线、推理服务分开目录
- 固定随机种子，保证可复现
- 记录实验：数据集、超参数、指标（用 `wandb` 或简单 CSV）
- 模型文件不提交 git：用 Release、模型仓库或对象存储

## 评估必看

- 分类：准确率、精确率、召回率、F1、混淆矩阵
- 检测：mAP
- 明确你的场景更看重哪个指标（如工业缺陷：漏检代价 > 误检）

## 下一步

- 视觉方向：[computer-vision.md](computer-vision.md)
- 工业落地：[industrial-vision.md](industrial-vision.md)
