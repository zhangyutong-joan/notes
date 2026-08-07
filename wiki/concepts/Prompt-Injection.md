---

type: concept
created: 2026-08-06
updated: 2026-08-06
sources: ["[[sources/Context_Engineering_223615]]"]
tags: [phenomenon]
aliases:
  - "提示注入"
  - "Prompt Injection Attack"
  - "直接提示注入"
sources:
  - [[sources/Context_Engineering_223615]]
generation_complete: true
---


# Prompt Injection

## 定义
Prompt Injection（提示注入）是一种针对以大语言模型为核心的 Agent 的安全攻击手段。攻击者利用 Agent 必须处理的外部不可信内容（如网页、邮件、文档等），将伪装成系统指令的文本混入模型的上下文中，从而覆盖或劫持 Agent 原本的行为，使其执行攻击者预期的恶意操作。

## 关键特征
- **指令与数据的混淆**：攻击本质在于大语言模型难以自行区分“系统指令”与“待处理的数据”，攻击者将恶意指令嵌入数据区域，模型会将其当作合法指令执行。
- **外部内容作为攻击载体**：攻击入口往往为 Agent 有权读取但无法完全控制的外部内容（如用户输入、检索到的文档、第三方 API 返回结果）。
- **静默且难以检测**：注入的指令通常不改变用户可见的界面，而是在后台悄悄改变 Agent 的行为逻辑，传统输入校验难以发现。
- **三种防御思路**：
  - **来源标记（Source Marking）**：用特定标签（如 `<external_content>...</external_content>`）包裹外部内容，并在 System Prompt 中明确声明该区域不可信，要求模型只视其为数据，不从中提取指令。
  - **Chat Template 角色机制**：严格使用 Chat Template（如 system / user / assistant / tool 角色），将系统指令固化在 `system` 角色中，将外部数据置于 `user` 或 `tool` 角色，通过角色边界分隔指令与数据。
  - **输入清洗**：对进入上下文的外部内容进行过滤、转义或限制长度，作为辅助防御手段。

## 应用
- **Agent 安全架构设计**：在构建基于 LLM 的应用时，通过结构化的 Context Engineering 显式标记可信指令和不可信数据的边界，是防止提示注入的第一道防线。
- **LLM 应用安全测试**：安全研究人员通过模拟提示注入攻击，检验应用是否存在越权操作或敏感信息泄露的风险。
- **内容审核与过滤系统**：在允许外部内容进入模型上下文之前，对其进行风险检测，但单独依赖输入清洗往往不足以应对复杂注入，需要与来源标记和角色机制配合。

## 相关概念
- [[concepts/Chat-Template|聊天模板]]
- [[concepts/System-Prompt|System Prompt]]
- [[concepts/source-marking|来源标记]]

## 相关实体
暂无直接相关实体。

## Mentions in Source
暂无直接引用内容。

## 来源提及

- "提示注入（Prompt Injection）：攻击者通过 Agent 处理的外部内容（网页、邮件、文档等），将伪装成系统指令的文本混入上下文，从而劫持 Agent 的行为。" (提示注入（Prompt Injection）：攻击者通过 Agent 处理的外部内容（网页、邮件、文档等），将伪装成系统指令的文本混入上下文，从而劫持 Agent 的行为。) — [[raw/concept_note/Context_Engineering|Context_Engineering]]