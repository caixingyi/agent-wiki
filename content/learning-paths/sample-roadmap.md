---
title: "示例：从 0 到 1 学习 AI Agent 的 6 个月路线"
type: docs
sidebar:
  open: false
---

> 这是一篇**模板文章**，演示「他山之石」板块的内容格式。请基于这个模板撰写你自己的故事。

## 背景

- **身份**：3 年经验的前端工程师
- **基础**：Python 入门级（写过爬虫），无机器学习背景
- **目标**：6 个月内能独立做一个 RAG Agent 项目，争取年底面试 AI 相关岗位

## 时间线

### 第 1 个月：补 Python + LLM 基础

**目标**：能流畅用 Python 调用 OpenAI / Claude API。

- 《Python 编程：从入门到实践》第 1-11 章（约 2 周）
- OpenAI Cookbook 走读：[github.com/openai/openai-cookbook](https://github.com/openai/openai-cookbook)
- 动手：写一个命令行翻译工具，支持上下文记忆

**踩坑**：一开始花太多时间看 Transformer 论文，其实做应用根本用不到那么深。

### 第 2 个月：Prompt Engineering + Function Calling

- [Prompt Engineering Guide](https://www.promptingguide.ai/zh)（约 1 周）
- 看 Andrew Ng 的 [ChatGPT Prompt Engineering for Developers](https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/) 短课
- 动手：用 Function Calling 做一个能查天气、查股票的小助手

### 第 3-4 个月：LangChain + RAG

- LangChain 官方文档完整过一遍
- 论文阅读：RAG 原始论文、Self-RAG、HyDE
- 动手：基于 LangChain + ChromaDB 做一个文档问答系统

**踩坑**：LangChain 抽象层级太高，建议先用原生 API 实现一遍 RAG 再用框架。

### 第 5 个月：Agent 框架对比

- 实操 LangGraph、CrewAI、AutoGen 各做一个小项目
- 阅读 [本站学习资源](/resources/) 中的框架对比

### 第 6 个月：完整项目 + 面试准备

- 选一个有商业价值的方向（客服 Agent / 代码助手 / 写作助手）做完整项目
- 刷 [本站面经](/interview/) 中的题目
- 投简历

## 用过的资源

| 类型 | 推荐 |
|------|------|
| 书 | 《大语言模型》（赵鑫等） |
| 课程 | DeepLearning.AI 的 [AI Agents 系列](https://www.deeplearning.ai/short-courses/) |
| 论文清单 | [Awesome-LLM-Agent](https://github.com/Paitesanshi/LLM-Agent-Survey) |

## 复盘

**走得顺**：
- 早期就开始动手写代码，不死磕理论
- 用真实项目驱动学习

**走了弯路**：
- 一开始尝试自己微调模型，浪费了 2 周
- LangChain 文档版本更新很快，老教程容易踩坑

---

*作者：示例 / 时间：2025-05*
