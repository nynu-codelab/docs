# RAG 入门

RAG（Retrieval-Augmented Generation，检索增强生成）：让大模型基于你自己的资料回答问题，减少幻觉。

## 为什么用 RAG

大模型不知道你的私有资料（实验室文档、项目数据、论文库）。RAG 把相关资料“喂”给模型再让它回答。

## 流程

```text
① 离线索引
   文档 → 切分(chunk) → 向量化(embedding) → 存入向量库

② 在线问答
   问题 → 向量化 → 检索最相关的 chunks → 拼进 Prompt → LLM 回答
```

## 三个关键环节

### 1. 切分（Chunking）

- 按段落 / 固定长度切块，一般 200-500 token
- 保留上下文：重叠一部分（overlap）
- 结构优先：按 Markdown 标题、代码块切分更准

### 2. 向量化（Embedding）

- 把文本变成向量，语义相近的向量距离近
- 用 OpenAI 兼容的 embedding 接口，`EMBEDDING_API_KEY=` 走 `.env`
- 中文场景注意模型对中文的支持

### 3. 检索与生成

- 检索：向量相似度（余弦相似度）取 Top-K
- 生成：把 chunks 拼进 prompt：

```text
基于以下资料回答问题：
<资料>
...
</资料>
问题：...
如果资料中没有答案，请直接说明不知道。
```

## 最小实现（不依赖向量数据库）

```python
class SimpleVectorStore:
    def __init__(self, embed_fn):
        self.embed_fn = embed_fn
        self.items = []  # (chunk, vector)

    def add(self, chunk: str):
        self.items.append((chunk, self.embed_fn(chunk)))

    def search(self, query: str, top_k: int = 3):
        qv = self.embed_fn(query)
        scored = sorted(
            self.items,
            key=lambda it: cosine(it[1], qv),
            reverse=True,
        )
        return [c for c, _ in scored[:top_k]]
```

数据量大了再换 Chroma / Milvus 等向量库。

## 评估

- 抽一批真实问题，看回答质量
- 关注：检索是否命中正确资料（Recall@K）、回答是否引用资料

## 在 CodeLab 实践

- 模板已内置简化版 RAG：[templates/ai-agent-template](https://github.com/nynu-codelab/templates/tree/main/ai-agent-template)
- 典型项目：实验室知识库问答、课程资料助手、论文阅读助手

## 下一步

- Agent + RAG 结合：[agent.md](agent.md)
