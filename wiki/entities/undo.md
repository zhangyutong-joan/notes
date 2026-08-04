---

type: entity
created: 2026-08-04
updated: 2026-08-04
sources: ["[[sources/Claude-code-命令_e53e82]]"]
tags: [other]
aliases:
  - "撤销修改命令"
  - "/undo 命令"
  - "撤销命令"
sources:
  - [[sources/Claude-code-命令_e53e82]]
generation_complete: true
---


# /undo

## 描述
`/undo` 是 [[entities/Claude-Code|Claude-Code]] 内置的[[concepts/斜杠命令|斜杠命令]]之一，专门用于撤销 Claude 在编辑过程中对文件所做的修改。当用户发现 Claude 的改动不符合预期，或者产生了意外的副作用时，可以通过输入该命令将文件恢复到修改前的状态，实现快速回退。该命令的设计理念类似于编辑器中的“撤销”功能或 [[concepts/版本控制|版本控制]] 系统中的 `revert` 操作，为 AI 辅助编程提供了即时的纠错手段。与之对应的恢复操作由 [[entities/redo|/redo]] 命令完成，用于重做被撤销的修改。

## 相关实体
- [[entities/Claude-Code|Claude-Code]] – 运行 `/undo` 命令的 CLI 工具
- [[entities/redo|/redo]] – 与此命令配对的“重做”命令

## 相关概念
- [[concepts/斜杠命令|斜杠命令]] – Claude Code 中的交互指令体系
- [[concepts/版本控制|版本控制]] – 回退修改的通用技术背景

## 来源提及

- "- `/undo`：撤销上一次文件修改（Claude 的修改效果不对时）" — [[Claude code 命令|Claude code 命令]]