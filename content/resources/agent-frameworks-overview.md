---
title: 主流 AI Agent 框架全面对比 (2025)
type: docs
weight: 1
sidebar:
  open: false
---

## 概述

随着 LLM 的快速发展，AI Agent 框架层出不穷。本文对比主流框架，帮助你选择合适的工具。

## 框架对比

| 框架 | 语言 | Multi-Agent | Tool Use | 亮点 |
|------|------|-------------|----------|------|
| **LangChain/LangGraph** | Python/JS | ✅ | ✅ | 生态最完善，社区最大 |
| **CrewAI** | Python | ✅ | ✅ | 角色驱动，上手简单 |
| **AutoGen** | Python | ✅ | ✅ | 微软出品，对话式协作 |
| **MetaGPT** | Python | ✅ | ✅ | SOP 驱动，结构化输出 |
| **Semantic Kernel** | C#/Python | ✅ | ✅ | 企业级，微软生态集成 |

## LangChain / LangGraph

LangChain 是目前最流行的 LLM 应用开发框架。LangGraph 是其图结构扩展，用于构建有状态的多步骤 Agent。

**适用场景：**
- 需要丰富的第三方集成
- 复杂的 RAG 管道
- 生产级应用

```python
from langgraph.graph import StateGraph

# 定义 Agent 状态和节点
graph = StateGraph(AgentState)
graph.add_node("agent", call_model)
graph.add_node("tools", tool_node)
```

## CrewAI

CrewAI 以"角色扮演"为核心理念，让多个 Agent 以团队协作的方式完成任务。

**适用场景：**
- 多角色协作任务
- 内容生成管道
- 快速原型开发

## 选型建议

- **初学者** → LangChain（文档最全）
- **多 Agent 协作** → CrewAI 或 AutoGen
- **企业级** → Semantic Kernel 或 LangGraph
- **研究探索** → MetaGPT

---

> 💡 **贡献指南**：如果你有框架使用经验，欢迎提交 PR 补充内容！
