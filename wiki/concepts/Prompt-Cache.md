---

type: concept
created: 2026-08-06
updated: 2026-08-06
sources: ["[[sources/Context_Engineering_223615]]"]
tags: [method]
aliases:
  - "提示缓存"
  - "Prompt Caching"
sources:
  - [[sources/Context_Engineering_223615]]
generation_complete: true
---


# Prompt Cache

## 定义
Prompt Cache 是 LLM API 服务层面的一种优化手段，旨在多次 API 请求之间复用相同前缀的已计算结果，从而降低计费成本和端到端延迟。与单次推理内部的 [[concepts/KV-Cache|KV Cache]] 不同，Prompt Cache 跨请求工作，要求多个请求共享完全一致的**前缀字节序列**。一旦前缀中任何字节被动态修改，缓存命中即告失败，性能退化至无缓存状态。

## 关键特征
- **跨请求复用**：缓存作用在连续多次 API 调用之间，而非单次推理内部
- **字节级稳定要求**：要求前缀内容（如系统提示词、工具定义）保持完全相同的字节序列，否则缓存失效
- **前缀敏感**：仅复用请求的共享前缀部分，后续不同部分无法利用缓存
- **强制设计约束**：为维持缓存命中，开发者必须将动态信息（如时间戳、用户状态）追加到对话末尾，避免插入前缀
- **降低延迟与成本**：成功命中后可减少重复计算，显著降低首 token 延迟和推理开销

## 应用
- **Agent 上下文设计**：将静态系统提示词、固定工具定义、角色设定等作为公共前缀，多个会话共享缓存
- **批量同构请求**：对大量具有相同长前缀的推理请求，如带相同系统指令的对话，可节省大量计算资源
- **API 优化策略**：结合 Provider 的 Prompt Caching 功能（如 Anthropic、OpenAI）设计请求结构，控制动态内容的放置位置
- **模板化对话**：将结构化模板（指令、示例）前置，动态用户输入后置，最大化缓存复用率

## 相关概念
- [[concepts/KV-Cache|KV Cache]]
- [[concepts/缓存一致性|缓存一致性]]
- [[concepts/动态系统提示词|动态系统提示词]]

## 来源提及

- "Prompt Cache：是 API 服务层的优化——跨多次 API 请求之间，缓存相同前缀的计算结果。" (Prompt Cache：是 API 服务层的优化——跨多次 API 请求之间，缓存相同前缀的计算结果。) — [[raw/concept_note/Context_Engineering|Context_Engineering]]