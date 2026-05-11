---
title: AI Agent 基础面试题 Top 20
type: docs
weight: 1
sidebar:
  open: false
---

## Q1: 什么是 AI Agent？与传统 Chatbot 的区别？

**参考答案：**

AI Agent 是一个能够感知环境、做出决策并采取行动的自主系统。与传统 Chatbot 的关键区别：

| 特性 | Chatbot | AI Agent |
|------|---------|----------|
| 自主性 | 被动响应 | 主动规划 |
| 工具使用 | 无 | 可调用外部工具 |
| 记忆 | 有限上下文 | 长期记忆 |
| 规划能力 | 无 | 任务分解与规划 |

## Q2: 解释 ReAct 模式

**参考答案：**

ReAct（Reasoning + Acting）是一种让 LLM 交替进行推理和行动的范式：

1. **Thought**：模型思考当前状态和下一步计划
2. **Action**：执行一个工具调用或操作
3. **Observation**：观察执行结果
4. 循环直到任务完成

```
Thought: 用户想知道今天北京天气，我需要调用天气 API
Action: weather_api(city="北京")
Observation: 晴天，25°C
Thought: 我已获得天气信息，可以回复用户了
Answer: 今天北京天气晴朗，气温 25°C。
```

## Q3: 什么是 Function Calling？

**参考答案：**

Function Calling 是 LLM 根据用户需求，结构化地输出函数调用参数的能力。模型不直接执行函数，而是返回函数名和参数的 JSON，由应用层执行。

## Q4: 如何处理 Agent 的幻觉问题？

**参考答案：**

- 使用 RAG 提供事实依据
- 在系统 prompt 中强调仅基于已知信息回答
- 添加事实验证步骤（Fact-checking Agent）
- 使用 Grounding 技术
- 设置适当的 temperature（偏低）

## Q5: Multi-Agent 系统的常见架构有哪些？

**参考答案：**

1. **中心化架构**：一个 Orchestrator Agent 协调其他 Agent
2. **去中心化架构**：Agent 之间对等通信
3. **层级架构**：类似组织架构的层级指挥
4. **市场机制**：Agent 通过竞价/拍卖分配任务

## Q6-Q20: 更多面试题

> 🔜 持续更新中...涵盖以下方向：
> - RAG 系统设计
> - Prompt Engineering
> - Agent Memory 机制
> - 工具编排与调度
> - Agent 评估与监控
> - 安全与对齐

---

> 💡 **贡献**：有面试经验想分享？欢迎提交 PR！
