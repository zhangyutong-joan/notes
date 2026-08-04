---
type: source
created: 2026-08-04
updated: 2026-08-04
source_file: "[[Claude code 命令]]"
tags:
  - note
aliases:
  - Claude Code 命令笔记
  - CC 常用命令
contentHash: 457-1e85227a
generation_complete: true
---

# Claude Code 常用命令 - Summary

## 来源
- Original file: [[Claude code 命令]]
- Ingested: 2026-08-04

## 核心内容
本笔记汇总了 [[entities/Claude-Code|Claude-Code]] 在终端与交互式会话中的常用命令，分为 [[concepts/CLI命令|CLI命令]] 和 [[concepts/斜杠命令|斜杠命令]] 两大类。CLI 命令（如 `claude -c`、`claude update`）在 PowerShell 环境下控制会话启动与版本更新；斜杠命令（如 `/help`、`/clear`、`/compact`）用于会话内的上下文管理与项目初始化。其中 `/init` 命令是核心工作流，它能自动生成 [[concepts/CLAUDE-md|CLAUDE-md]] 项目上下文文件，避免每次对话从零开始理解项目，从而统一团队行为、减少重复沟通。

笔记还记录了实用技巧：使用 `@` 符号 [[concepts/`@`-文件指定|`@`-文件指定]] 引用文件，利用 [[concepts/多模态输入|多模态输入]] 直接粘贴截图，以及当回答截断时输入 [[concepts/继续|继续]] 让 Claude 补全内容。内容来源于 [[entities/菜鸟教程|菜鸟教程]]，适合快速查阅。

## 关键实体
- [[entities/Claude-Code|Claude-Code]] – 命令行 AI 编程助手
- [[entities/菜鸟教程|菜鸟教程]] – 学习资料来源
- [[entities/compact|compact]] – 压缩上下文命令
- [[entities/resume|resume]] – 恢复历史对话命令
- [[entities/undo|undo]] – 撤销文件修改命令
- [[entities/redo|redo]] – 重做被撤销的修改
- [[entities/cost|cost]] – 查看 Token 用量命令

## 关键概念
- [[concepts/CLI命令|CLI命令]] – 终端层面控制 Claude Code 的指令
- [[concepts/斜杠命令|斜杠命令]] – 交互式会话内以 `/` 开头的内建指令
- [[concepts/CLAUDE-md|CLAUDE-md]] – 存储项目约定与上下文的配置文件
- [[concepts/init|init]] – 生成 CLAUDE.md 的项目初始化命令
- [[concepts/多模态输入|多模态输入]] – 可直接粘贴截图的多模态交互
- [[concepts/`@`-文件指定|`@`-文件指定]] – 用 `@` 引用项目文件
- [[concepts/继续|继续]] – 补全被截断回答的交互技巧

## 要点
- Claude Code 提供 CLI 命令和斜杠命令两套体系，分别控制会话启动与内部操作。
- `/init` 命令是项目初始化的核心，生成 [[concepts/CLAUDE-md|CLAUDE-md]] 以固化项目知识，减少重复沟通。
- [[concepts/CLAUDE-md|CLAUDE-md]] 能够统一团队行为、降低出错概率，维护时应保持精简并使用命令式语言。
- 支持多模态输入和 `@` 文件引用，提升信息传递效率。
- 善用“继续”可让 Claude 补充未完成的回答。