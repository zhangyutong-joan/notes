---

type: entity
created: 2026-08-04
updated: 2026-08-04
sources: ["[[sources/Claude-code-命令_e53e82]]"]
tags: [other]
aliases:
  - "/cost 命令"
  - "Token用量查看"
  - "token用量查询"
sources:
  - [[sources/Claude-code-命令_e53e82]]
generation_complete: true
---


# /cost

## 描述
/cost 是 [[entities/Claude-Code|Claude-Code]] 中的一条信息查询型[[concepts/斜杠命令|斜杠命令]]，用于实时反馈当前会话已消耗的 Token 数量。通过该命令，用户可以快速掌握对话的累计用量，从而评估 API 调用费用或判断是否需要进行上下文压缩（如执行 [[entities/compact|compact]] 命令）。该命令输出当前会话的输入/输出 Token 统计，帮助用户在长时间交互中保持对资源消耗的可视化控制。在 Claude‑Code 的命令参考文档中，该命令的功能被概括为“查看本次会话的 Token 用量”。

## 相关实体
- [[entities/Claude-Code|Claude-Code]] — /cost 的运行环境
- [[entities/compact|compact]] — 与 /cost 配合使用的上下文压缩命令

## 相关概念
- [[concepts/斜杠命令|斜杠命令]] — /cost 所属的命令类型

## 来源提及

- "- `/cost`：查看本次会话的 Token 用量" — [[Claude code 命令|Claude code 命令]]