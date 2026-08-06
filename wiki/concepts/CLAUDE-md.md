---
type: concept
created: 2026-08-04
updated: 2026-08-05
generation_complete: true
sources:
  - "[[sources/Claude-code-命令_e53e82]]"
  - "[[sources/llm-wiki_38393a]]"
tags:
  - "term"
aliases:
  - "Claude 项目配置文件"
  - "CLAUDE 文件"
  - "项目上下文文件"
---

## 相关概念
[[concepts/init|/init]]
[[concepts/斜杠命令|斜杠命令]]
[[concepts/LLM-Wiki|LLM-Wiki]]
[[concepts/RAG|RAG]]

## 相关实体
[[entities/Claude-Code|Claude-Code]]
[[entities/Obsidian|Obsidian]]

## 定义
CLAUDE.md 是 [[entities/Claude-Code|Claude-Code]] 用来存储项目上下文与约定的一份 Markdown 文件，通常由 `/init` 命令在项目根目录自动生成。它的核心价值在于将项目知识一次性文档化，使 AI 在每次对话中都能自动遵守团队规范，无需重复沟通。

## 关键特征
- **统一团队行为**：所有成员与 Claude 遵循相同的项目规范，避免理解偏差。
- **减少重复沟通**：包管理器、代码风格、测试命令等约定只写一次，不再需要每次对话时重复说明。
- **降低出错概率**：可在文件中明确告知 Claude 哪些操作存在风险，防止误修改。
- **加速 AI 理解**：帮助 Claude 快速定位关键文件、项目结构和依赖关系。
- **可维护的知识固化**：将人与 AI 之间的重复沟通成本转移到一次性文档编写中，建议保持内容精简、持续更新并使用命令式语言。

## 应用
- 在 [[entities/Claude-Code|Claude-Code]] 工作流中，作为项目级 AI 助手的“使用说明书”。
- 适用于任何需要 AI 长期参与维护、开发或分析的项目，可固化项目约定、环境配置与常见陷阱。
- 与 `/init` 命令配合使用，在项目初始化时自动生成或更新。

## 来源提及

- "没有 `CLAUDE.md` 时，Claude 每次都从零开始理解你的项目，你需要反复告诉它：用哪个包管理器、代码风格是什么、测试怎么跑、哪些文件不要动……" (没有 CLAUDE.md 时，Claude 每次都从零开始理解你的项目，你需要反复告诉它：用哪个包管理器、代码风格是什么、测试怎么跑、哪些文件不要动……) — [[Claude code 命令|Claude code 命令]]
- "有了 `CLAUDE.md`，这些信息只需写一次，Claude 每次都会遵守。" (有了 CLAUDE.md，这些信息只需写一次，Claude 每次都会遵守。) — [[Claude code 命令|Claude code 命令]]
- "`CLAUDE.md` 可以帮你做到以下几件事：统一团队行为、减少重复沟通、降低出错概率、加速 AI 理解。" (CLAUDE.md 可以帮你做到以下几件事：统一团队行为、减少重复沟通、降低出错概率、加速 AI 理解。) — [[Claude code 命令|Claude code 命令]]