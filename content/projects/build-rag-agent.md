---
title: "实战：从零构建一个 RAG Agent"
type: docs
weight: 1
sidebar:
  open: false
---

## 项目简介

构建一个能够：
1. 加载和处理 PDF/Markdown 文档
2. 创建向量索引
3. 基于检索结果回答问题
4. 支持多轮对话

## 技术栈

- **LLM**: OpenAI GPT-4o / 本地模型
- **框架**: LangChain + LangGraph
- **向量库**: ChromaDB
- **Embedding**: text-embedding-3-small
- **前端**: Streamlit

## 项目结构

```
rag-agent/
├── app.py              # Streamlit 主应用
├── agent/
│   ├── graph.py        # LangGraph Agent 定义
│   ├── tools.py        # 检索工具
│   └── prompts.py      # Prompt 模板
├── ingestion/
│   ├── loader.py       # 文档加载器
│   └── processor.py    # 分块和 Embedding
├── requirements.txt
└── README.md
```

## 核心代码

### 文档加载与处理

```python
from langchain_community.document_loaders import PyPDFLoader
from langchain.text_splitter import RecursiveCharacterTextSplitter
from langchain_chroma import Chroma
from langchain_openai import OpenAIEmbeddings

def ingest_documents(file_path: str):
    loader = PyPDFLoader(file_path)
    docs = loader.load()

    splitter = RecursiveCharacterTextSplitter(
        chunk_size=512,
        chunk_overlap=50
    )
    chunks = splitter.split_documents(docs)

    vectorstore = Chroma.from_documents(
        documents=chunks,
        embedding=OpenAIEmbeddings(model="text-embedding-3-small"),
        persist_directory="./chroma_db"
    )
    return vectorstore
```

### Agent 构建

```python
from langgraph.graph import StateGraph, END
from langchain_openai import ChatOpenAI

def create_rag_agent(vectorstore):
    retriever = vectorstore.as_retriever(search_kwargs={"k": 5})
    llm = ChatOpenAI(model="gpt-4o", temperature=0)

    # 定义 Agent 状态图
    graph = StateGraph(AgentState)
    graph.add_node("retrieve", retrieve_node)
    graph.add_node("generate", generate_node)
    graph.add_node("evaluate", evaluate_node)

    graph.set_entry_point("retrieve")
    graph.add_edge("retrieve", "generate")
    graph.add_conditional_edges("evaluate", should_retry)

    return graph.compile()
```

## 运行方式

```bash
pip install -r requirements.txt
streamlit run app.py
```

## 扩展方向

- 添加 Web 搜索工具
- 支持多文档来源（Notion、Confluence）
- 添加对话历史持久化
- 部署到云端

---

> 📦 **完整代码**：[GitHub 仓库链接](https://github.com/YOUR_USERNAME/rag-agent-demo)
