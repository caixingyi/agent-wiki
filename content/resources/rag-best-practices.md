---
title: RAG 最佳实践指南
type: docs
weight: 2
sidebar:
  open: false
---

## 什么是 RAG？

RAG（Retrieval-Augmented Generation）是将检索系统与 LLM 结合的技术，让模型能基于外部知识库回答问题。

## 核心流程

```
文档 → 分块 → Embedding → 向量存储 → 查询检索 → LLM 生成
```

## 1. 文档处理与分块

### 分块策略

- **固定大小分块**：简单但可能切断语义
- **语义分块**：基于语义边界切分，效果更好
- **递归分块**：LangChain 默认策略，按层级分隔符切分

```python
from langchain.text_splitter import RecursiveCharacterTextSplitter

splitter = RecursiveCharacterTextSplitter(
    chunk_size=512,
    chunk_overlap=50,
    separators=["\n\n", "\n", "。", "，", " "]
)
```

### 建议

- chunk_size 推荐 256-1024 tokens
- chunk_overlap 保持 10-20%
- 保留元数据（来源、标题、页码等）

## 2. Embedding 模型选择

| 模型 | 维度 | 中文支持 | 推荐场景 |
|------|------|----------|----------|
| text-embedding-3-large | 3072 | ✅ | 通用首选 |
| bge-large-zh | 1024 | ✅ | 中文专项 |
| GTE-Qwen2 | 多种 | ✅ | 开源最佳 |

## 3. 检索策略

- **混合检索**：向量 + BM25 关键词检索
- **重排序**：使用 Cross-Encoder 对检索结果重排
- **查询改写**：用 LLM 改写用户查询提高召回率

## 4. 常见问题

- **幻觉问题**：在 prompt 中强调"仅基于提供的上下文回答"
- **多跳问答**：使用 Agentic RAG，让 Agent 多次检索
- **长文档**：考虑 Map-Reduce 或分层摘要

---

> 📖 推荐阅读：[RAG Survey Paper](https://arxiv.org/abs/2312.10997)
