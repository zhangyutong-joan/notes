---

type: concept
created: 2026-08-06
updated: 2026-08-06
sources: ["[[sources/Context_Engineering_223615]]"]
tags: [method]
aliases:
  - "子Agent对齐"
  - "字节级对齐"
sources:
  - [[sources/Context_Engineering_223615]]
generation_complete: true
---


# Sub-agent alignment

## 定义
**Sub-agent alignment（子Agent对齐）** 是从上下文工程的[[concepts/缓存一致性|缓存一致性]]原则衍生出的一种架构约束，它要求每一个子 Agent 的提示词（system prompt）、工具定义（tool definitions）、模型配置（model configuration）、消息前缀（message prefix）和思考配置（thinking configuration）与父 Agent 保持逐字节完全一致。该约束的唯一目的是保证子 Agent 发出的 API 请求前缀与父 Agent 匹配，从而能够命中服务商的 [[concepts/Prompt-Cache|Prompt Cache]]（Prompt Cache）及底层的 [[concepts/KV-Cache|KV Cache]]，大幅降低推理计费和首 token 延迟。

## 关键特征
- **字节级严格匹配**：所有影响请求前缀的组件（提示词、工具定义、模型参数等）必须与父 Agent 逐字节相同，不允许任何偏差。
- **缓存命中驱动架构**：设计决策从缓存层向上传导，Agent 的生成方式、参数传递机制完全围绕缓存命中率优化。
- **上下文工程优先**：属于“缓存优先设计”的典型实践，是 [[concepts/缓存一致性|缓存一致性]] 在多 Agent 协同场景中的直接应用。
- **前缀对齐**：不仅要求内容一致，还要求消息顺序与结构（如聊天模板）一致，以确保前缀的哈希值完全重合。

## 应用
- **多 Agent 系统**：当存在大量子 Agent 执行相似任务时，通过 Sub-agent alignment 可显著降低总体推理成本与延迟。
- **工具链协同**：在需要多个具有相同工具集、相同系统行为的 Agent 协同工作时，保证缓存复合利用。
- **上下文工程架构**：作为设计原则指导 Agent 框架的开发，将缓存友好性嵌入到 Agent 生命周期管理中。

## 相关概念
- [[concepts/缓存一致性|缓存一致性]]
- [[concepts/Prompt-Cache|Prompt Cache]]
- [[concepts/KV-Cache|KV Cache]]

## 相关实体
- （暂无直接相关实体）

## 来源提及

- "子 Agent 必须与父 Agent 字节级对齐。当主 Agent 派生子 Agent 或进行旁路查询时，子 Agent 的提示词、工具定义、模型配置、消息前缀和思考配置必须与父 Agent 的缓存键逐字节匹配。" — [[raw/concept_note/Context_Engineering|Context_Engineering]]
- "这样做的原因是：子 Agent 发起的 API 请求如果前缀与父 Agent 的请求一致，就能命中 API 服务商的 Prompt Cache，从而减少计费和延迟。" — [[raw/concept_note/Context_Engineering|Context_Engineering]]