---

type: concept
created: 2026-08-04
updated: 2026-08-04
sources: ["[[sources/Claude-code-命令_e53e82]]"]
tags: [method]
aliases:
  - "初始化命令"
  - "/init 命令"
  - "init 命令"
sources:
  - [[sources/Claude-code-命令_e53e82]]
generation_complete: true
---


# /init

## 定义
/init 是 [[entities/Claude-Code|Claude Code]] 提供的一个 [[concepts/斜杠命令|斜杠命令]]，用于**初始化项目上下文**。执行该命令后，Claude 会自动扫描当前项目的代码结构、工具链和约定，并生成一份 `CLAUDE.md` 文件，将所有关键信息沉淀为项目级记忆。后续的每次对话都会自动读取该文件，使 AI 助手无需用户重复说明即可掌握项目环境。

## 关键特征
- 属于 Claude Code 的内置[[concepts/斜杠命令|斜杠命令]]，直接在 CLI 交互中键入 `/init` 即可触发
- **自动项目扫描**：分析语言、框架、构建工具、目录布局等重要项目特征
- **生成 `CLAUDE.md`**：将扫描结果写入项目根目录下的 `CLAUDE.md`，文件没有强制格式要求
- **单向一次性指南**：通常在新项目第一次使用时运行，充当“项目初始化向导”
- **持续上下文支持**：生成的 `CLAUDE.md` 会被 Claude 在每个会话开始时自动加载，使助手持续理解项目约定
- **无侵入**：只是生成一个文本文件，不会修改项目代码或配置文件

## 应用
- **新项目上手**：克隆或新建项目后，通过 `/init` 让 Claude 快速建立对项目的整体认知
- **团队统一上下文**：团队成员在不同机器上使用 Claude Code 时，运行 `/init` 以保持一致的辅助基线
- **减少重复解释**：避免每次会话都要手动说明“项目用什么技术栈”、“测试怎么跑”等信息
- **逐步完善上下文**：当项目结构或工具链发生变化时，可重新运行 `/init` 更新 `CLAUDE.md`，或手动编辑该文件

## 相关概念
- [[concepts/斜杠命令|斜杠命令]] —— Claude Code 命令体系，/init 是其中的项目初始化命令
- [[concepts/CLAUDE.md|CLAUDE.md]] —— /init 命令生成的项目上下文文件，承载项目记忆
- [[concepts/CLI命令|CLI命令]] —— /init 在命令行界面中执行的更广泛命令上下文

## 相关实体
- [[entities/Claude-Code|Claude Code]] —— 提供 /init 命令的 AI 编程助手工具
- [[entities/cost|cost]] —— 另一个关键的 Claude Code 斜杠命令，用于查询 token 用量
- [[entities/compact|compact]] —— 用于压缩对话上下文的 Claude Code 斜杠命令
- [[entities/undo|undo]] / [[entities/redo|redo]] —— 与 /init 同一体系下的对话操作命令

## 来源提及

- "`/init`：分析项目并生成 **CLAUDE.md 文件**（首次在新项目中使用），没有强制的格式要求" (/init：分析项目并生成 CLAUDE.md 文件（首次在新项目中使用），没有强制的格式要求) — [[Claude code 命令|Claude code 命令]]