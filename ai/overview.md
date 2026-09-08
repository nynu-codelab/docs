# AI 方向概述

CodeLab 算法部（AI 方向）做什么：基于大模型与机器学习做真实可用的应用，而不是只跑 demo。

## 方向范围

- **AI / Agent 开发**：调用大模型构建能“干活”的智能体
- **计算机视觉**：图像分类、目标检测、分割等
- **工业视觉**：缺陷检测、字符识别（OCR）等落地场景
- **机器学习基础**：模型训练、评估、调优

## 基础环境

- Python 3.12 + uv（见 [python.md](../software/python.md)）
- PyTorch（视觉/训练）
- 大模型 API：各家 OpenAI 兼容接口，密钥走 `.env`

## CodeLab 的做法

1. **先明确问题**：要解决什么、数据从哪来、怎么评估效果
2. **从简单方案开始**：先接 API / 用现成模型跑通，再优化
3. **工程化交付**：代码进 GitHub、有测试、能 Docker 部署
4. **成果沉淀**：模型、数据集、论文、专利由成果中心登记

## 通用管线

```text
数据收集 → 数据清洗/标注 → 模型（训练/微调/API）
  → 评估（指标、badcase）→ 服务化（FastAPI + Docker）→ 交付
```

## 下一步

- Agent 怎么开发：[agent.md](agent.md)
- RAG 是什么：[rag.md](rag.md)
- 用 [ai-agent-template](https://github.com/nynu-codelab/templates/tree/main/ai-agent-template) 起步
