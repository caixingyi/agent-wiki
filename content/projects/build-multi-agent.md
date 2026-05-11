---
title: "实战：用 CrewAI 搭建多 Agent 协作系统"
type: docs
weight: 2
sidebar:
  open: false
---

## 项目简介

用 CrewAI 构建一个**自动技术调研助手**，由 3 个 Agent 协作完成：
1. **搜索 Agent**：根据主题在网上检索资料
2. **分析 Agent**：整理和提炼关键信息
3. **写作 Agent**：输出一份结构化的调研报告

## 技术栈

- **框架**: CrewAI
- **LLM**: OpenAI GPT-4o
- **工具**: SerperDevTool（搜索）、ScrapeWebsiteTool（网页抓取）

## 核心代码

### 定义 Agent

```python
from crewai import Agent, Task, Crew

searcher = Agent(
    role="技术搜索专家",
    goal="根据给定主题，搜索最新、最相关的技术资料",
    backstory="你是一名资深技术情报分析师，擅长从海量信息中快速定位高价值内容。",
    tools=[SerperDevTool(), ScrapeWebsiteTool()],
    verbose=True
)

analyst = Agent(
    role="技术分析师",
    goal="从搜索结果中提炼关键信息，梳理技术脉络",
    backstory="你是一名有 10 年经验的技术架构师，擅长对比分析不同技术方案。",
    verbose=True
)

writer = Agent(
    role="技术写作专家",
    goal="将分析结果整理成结构清晰、易读的调研报告",
    backstory="你是一名技术博主，文章风格简洁有力，擅长用表格和图示说明问题。",
    verbose=True
)
```

### 定义任务

```python
search_task = Task(
    description="搜索关于 {topic} 的最新技术动态、框架对比、最佳实践，至少找到 5 个高质量来源。",
    expected_output="包含标题、链接、摘要的资料列表",
    agent=searcher
)

analysis_task = Task(
    description="基于搜索结果，分析各方案的优缺点、适用场景和发展趋势。",
    expected_output="结构化的对比分析，包含表格",
    agent=analyst
)

writing_task = Task(
    description="基于分析结果，撰写一份 1500 字左右的技术调研报告。",
    expected_output="Markdown 格式的调研报告",
    agent=writer,
    output_file="report.md"
)
```

### 组装 Crew

```python
crew = Crew(
    agents=[searcher, analyst, writer],
    tasks=[search_task, analysis_task, writing_task],
    verbose=True
)

result = crew.kickoff(inputs={"topic": "2025 年 AI Agent 框架对比"})
print(result)
```

## 运行

```bash
pip install crewai crewai-tools
export OPENAI_API_KEY="sk-..."
export SERPER_API_KEY="..."
python main.py
```

## 学到什么

- **角色设计**：每个 Agent 的 `role` 和 `backstory` 直接影响输出质量
- **任务链**：后一个任务自动接收前一个任务的输出，形成流水线
- **工具分配**：只给需要的 Agent 配工具，避免不必要的调用

## 扩展方向

- 加入 Human-in-the-loop：分析完后让用户确认再写报告
- 支持中文搜索（接入百度/必应 API）
- 输出 PDF 格式报告
- 增加代码示例 Agent，自动跑 demo

---

> 📦 **完整代码**：[GitHub 仓库链接](https://github.com/YOUR_USERNAME/crewai-research-demo)（欢迎 PR 补充）
