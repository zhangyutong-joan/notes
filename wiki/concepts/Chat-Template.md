---

type: concept
created: 2026-08-06
updated: 2026-08-06
sources: ["[[sources/context-engineering]]"]
tags: [standard]
aliases:
  - "聊天模板"
sources:
  - [[sources/Context_Engineering_223615]]
generation_complete: true
---


# Chat Template

## 定义
Chat Template（聊天模板）是一种将对话角色（system、user、assistant、tool）与消息内容转换为固定 token 序列的标准化格式。该模板通常由模型训练时的分词与顺序规则决定，定义了不同角色标记在 token 序列中的布局，从而为 LLM 推理提供了可预测的文本表达结构。

## 关键特征
- **角色感知编码**：将 system、user、assistant、tool 四种角色的消息分别封装为带有角色指示符的 token 块，使模型能从 token 序列中还原对话边界。
- **前缀固定机制**：system 消息和工具定义被编码为序列最前端的 token，天然形成了 KV Cache 的前缀边界。模板之前的任何 token 变动都会导致整个缓存失效，从而强制实现前缀稳定性。
- **缓存依赖**：解释了为何动态修改系统提示词会破坏 Prompt Cache——模板赋予系统提示词特殊的起始位置，任何变更都会重新编码整个前缀。
- **安全隔离**：严格利用 Chat Template 的角色体系将指令与外部数据分离，模型通过角色标记区分可信指令和不可信内容，因此是防御提示注入的有效工程手段之一。

## 应用
- **LLM 推理服务**：在 vLLM、Hugging Face TGI 等框架中，Chat Template 被用于将对话历史格式化为模型可接受的 prompt。
- **缓存优化**：通过模板约束前缀结构，实现 Prompt Cache 的精准复用，仅缓存不变的前缀部分，提升推理吞吐量。
- **提示注入防御**：利用模板强制划分角色边界，阻止用户输入跨越角色标记污染系统指令。

## 相关概念
- [[concepts/KV-Cache|KV Cache]]
- [[concepts/Prompt-Cache|Prompt Cache]]
- [[concepts/提示注入|提示注入]]
- [[concepts/System-Prompt|System Prompt]]

## 相关实体
暂无直接关联实体。

## Mentions in Source
暂无直接引用记录（页面基于上下文工程知识构建）。

## 来源提及

- "Chat Template 解释了 KV Cache 为什么对前缀如此敏感。Chat Template 将 system 消息和工具定义转换为固定的 token 序列放在最前面。" (Chat Template 解释了 KV Cache 为什么对前缀如此敏感。Chat Template 将 system 消息和工具定义转换为固定的 token 序列放在最前面。) — [[raw/concept_note/Context_Engineering|Context_Engineering]]