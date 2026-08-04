---

type: entity
created: 2026-08-04
updated: 2026-08-04
sources: ["[[sources/Claude-code-命令_e53e82]]"]
tags: [other]
aliases:
  - "重做修改命令"
  - "/redo 命令"
sources:
  - [[sources/Claude-code-命令_e53e82]]
generation_complete: true
---


# /redo

## 描述

/redo 是 [[entities/Claude-Code|Claude-Code]] 中的一条斜杠命令，专门用于重做刚被撤销的文件修改。当用户使用 [[entities/undo|/undo]] 撤销了 Claude 自动生成的代码或文档更改后，如果发现撤销后的结果反而不如原来的修改，可以通过该命令将已撤销的更改恢复回来。/redo 与 /undo 构成了一对反向操作，为开发者提供了更大的容错空间，使其能够更灵活地管理 [[concepts/斜杠命令|斜杠命令]] 驱动的 AI 编辑结果。在 Claude Code 的命令文档中，它的作用被描述为“重做被撤销的修改（撤销后发现还是原来的好）”。

## 相关实体

- [[entities/Claude-Code|Claude-Code]]
- [[entities/undo|/undo]]

## 相关概念

- [[concepts/斜杠命令|斜杠命令]]

## 来源提及

- "- `/redo`：重做被撤销的修改（撤销后发现还是原来的好）" — [[Claude code 命令|Claude code 命令]]