---
type: concept
created: 2026-08-07
updated: 2026-08-07
generation_complete: true
sources:
  - "[[sources/上下文整理助手_bb5677]]"
  - "[[sources/notes_795b78]]"
tags:
  - "term"
aliases:
  - "任务提示"
  - "Your prompt"
---

## 相关概念
- [[concepts/上下文整理助手|上下文整理助手]]
- [[concepts/Memory|Memory]]
- [[concepts/Skills|Skills]]
- [[concepts/References|References]]
- [[concepts/上下文工程|上下文工程]]

## 相关实体
无（暂无特定实体关联）

## 定义
「Your prompt」是用户在一次对话中提交的具体任务指令，代表 Agent 本次需要执行的操作。它是每轮对话的暂态信息，与长期项目上下文（如 CLAUDE.md）、个人偏好（Memory）和可复用技能（Skills）有本质区别。在[[concepts/上下文整理助手|上下文整理助手]]的梳理过程中，需要将这部分识别并提取出来，以确保 Agent 明确当前的任务目标，避免任务混淆。

## 关键特征
- **会话暂态性**：仅存在于当前对话轮次，任务完成后即失效。
- **任务指向性**：直接描述“要做什么”，区别于“偏好是什么”或“长期环境是什么”。
- **独立清晰性**：强调单次任务的专注度，防止与历史任务或长期设定掺杂。
- **区别于长期上下文**：与 [[concepts/Memory|Memory]]（持久化偏好）、[[concepts/Skills|Skills]]（可复用指令集）和项目级文件（如 CLAUDE.md）形成互补的分层 Context 结构。

## 应用
- **助手任务提取**：[[concepts/上下文整理助手|上下文整理助手]] 在整理上下文时，自动抓取当前提示中的任务指令，作为后续推理和行动的核心依据。
- **上下文组装**：在[[concepts/上下文工程|上下文工程]]中，将 Your prompt 与个人记忆、技能包等模块化内容动态组合，生成精准的模型输入。
- **多任务切换**：当用户在对话中连续给出不同任务时，通过区分每个 Your prompt 来维持执行边界的清晰。

## 来源提及

- "1. Your prompt：我这次具体想让 Agent 做什么（单次任务）" — [[raw/prompt_pool/notes|notes]]
- "你需要带我梳理 6 类信息：" — [[raw/prompt_pool/notes|notes]]
- "**Your prompt：** 告诉 Agent 这次具体要做什么" (**用户提示词：** 告诉 Agent 这次具体要做什么) — [[raw/prompt_pool/notes|notes]]