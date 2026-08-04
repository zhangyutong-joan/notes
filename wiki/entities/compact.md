---

type: entity
created: 2026-08-04
updated: 2026-08-04
sources: ["[[sources/Claude-code-命令_e53e82]]"]
tags: [other]
aliases:
  - "compact 命令"
  - "/compact 命令"
  - "compact 指令"
sources:
  - [[sources/Claude-code-命令_e53e82]]
generation_complete: true
---


# /compact

## 描述
`/compact` 是 [[entities/claude-code|Claude Code]] 提供的一个[[concepts/斜杠命令|斜杠命令]]，用于压缩当前对话上下文以释放空间。当对话历史累积过多文本、逼近上下文窗口限制时，用户执行该命令可以修剪冗余信息，同时保留对话的核心内容，从而在不超出限制的情况下继续对话。与直接清除历史的 `/clear` 命令不同，`/compact` 通过智能压缩减少上下文占用的令牌数，提升后续交互的响应速度和效率。该命令是 Claude Code 对话管理工具集的一部分，帮助用户在长时间会话中维持流畅的协作体验。

## 相关实体
- [[entities/claude-code|Claude Code]]

## 相关概念
- [[concepts/斜杠命令|斜杠命令]]

## 来源引用
- “/compact：压缩当前对话上下文，释放空间。” — [[sources/Claude-code-命令_e53e82]]

## 来源提及

- "- `/compact`：压缩当前对话上下文，释放空间" — [[Claude code 命令|Claude code 命令]]