---
title: "面试题：Agent 记忆系统设计"
type: docs
weight: 3
sidebar:
  open: false
---

## 题目背景

Agent 的记忆系统是区别于普通 Chatbot 的关键能力。面试中经常会围绕记忆系统的设计和实现展开提问。

## Q1: Agent 的记忆系统有哪几种类型？

**参考答案：**

| 类型 | 说明 | 类比 | 存储方式 |
|------|------|------|----------|
| **短期记忆** | 当前对话的上下文 | 工作记忆 | 对话历史（内存/Redis） |
| **长期记忆** | 跨会话的持久化知识 | 经验记忆 | 向量数据库/关系型数据库 |
| **情景记忆** | 过去交互的具体片段 | 回忆特定事件 | 向量数据库 |
| **语义记忆** | 抽象化的知识和规则 | 常识 | 知识图谱/结构化数据 |
| **程序记忆** | 学到的技能和操作流程 | 肌肉记忆 | 工具定义/SOP |

## Q2: 如何实现 Agent 的长期记忆？

**参考答案：**

核心流程：

```
对话结束
  ↓
[摘要提取] — 从对话中提取关键信息
  ↓
[Embedding] — 转为向量表示
  ↓
[存储] — 写入向量数据库（Pinecone/Milvus/Chroma）
  ↓
下次对话开始时
  ↓
[检索] — 用当前问题检索相关记忆
  ↓
[注入 Prompt] — 把检索结果作为上下文传给 LLM
```

代码示例：

```python
from langchain.memory import VectorStoreRetrieverMemory
from langchain_chroma import Chroma
from langchain_openai import OpenAIEmbeddings

# 创建向量存储
vectorstore = Chroma(
    embedding_function=OpenAIEmbeddings(),
    persist_directory="./memory_db"
)

# 创建记忆
memory = VectorStoreRetrieverMemory(
    retriever=vectorstore.as_retriever(search_kwargs={"k": 3})
)

# 保存记忆
memory.save_context(
    {"input": "我是做前端开发的"},
    {"output": "好的，了解你的技术背景是前端开发。"}
)

# 检索记忆
relevant_memories = memory.load_memory_variables(
    {"prompt": "推荐适合我的 Agent 学习路线"}
)
# 会自动检索到"用户是前端开发"这条记忆
```

## Q3: 短期记忆的上下文窗口用满了怎么办？

**参考答案：**

几种常见策略：

1. **滑动窗口**：只保留最近 N 轮对话
2. **对话摘要**：用 LLM 把历史对话压缩成摘要
3. **混合策略**：最近 5 轮保留原文 + 更早的做摘要
4. **Token 预算**：动态计算 token 用量，超出时压缩最旧的内容

**追问：摘要策略的缺点是什么？**

- 摘要过程本身消耗 token 和延迟
- 摘要可能丢失细节信息
- 需要额外一次 LLM 调用

## Q4: 如何评估记忆系统的效果？

**参考答案：**

| 指标 | 说明 |
|------|------|
| **召回准确率** | 检索到的记忆是否与当前问题相关 |
| **时效性** | 是否优先召回最新最相关的信息 |
| **一致性** | 多次查询同一信息返回结果是否稳定 |
| **遗忘曲线** | 旧记忆是否被合理淘汰 |

---

> 💡 **贡献**：有记忆系统相关的面试经历？欢迎 PR 补充真题和答案！
