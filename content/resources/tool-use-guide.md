---
title: Agent Tool Use 完全指南
type: docs
weight: 3
sidebar:
  open: false
---

## 什么是 Tool Use？

Tool Use 是 Agent 的核心能力之一 —— 让 LLM 能够调用外部工具（API、数据库、代码执行器等）来完成无法仅通过语言完成的任务。

## 演进历程

```
Prompt Hacking → Function Calling → Tool Use → MCP
(2023 初)        (2023 中)          (2024)      (2025)
```

## Function Calling

OpenAI 率先推出的结构化工具调用方式：

```python
tools = [{
    "type": "function",
    "function": {
        "name": "get_weather",
        "description": "获取指定城市的天气信息",
        "parameters": {
            "type": "object",
            "properties": {
                "city": {"type": "string", "description": "城市名"},
                "unit": {"type": "string", "enum": ["celsius", "fahrenheit"]}
            },
            "required": ["city"]
        }
    }
}]
```

## MCP（Model Context Protocol）

Anthropic 推出的开放标准，统一 Agent 与工具的通信协议：

- **标准化**：统一的工具描述和调用格式
- **可发现**：工具可以被 Agent 自动发现
- **安全**：内置权限控制和审计

## 最佳实践

1. **工具描述要清晰** — 直接影响 LLM 选择工具的准确性
2. **参数校验** — 永远不要信任 LLM 输出的参数
3. **错误处理** — 工具失败时提供有意义的错误信息
4. **最小权限** — 每个工具只暴露必要的能力
5. **幂等设计** — 确保重复调用不会造成副作用

---

> 🔗 参考：[MCP 官方文档](https://modelcontextprotocol.io)
