---

type: concept
created: 2026-08-05
updated: 2026-08-05
sources: ["[[sources/llm-wiki_38393a]]"]
tags: [term]
aliases:
  - "Wiki Schema配置"
  - "LLM Wiki规则文件"
  - "Schema 文件"
sources:
  - [[sources/llm-wiki_38393a]]
generation_complete: true
---


# Schema

## 定义
Schema 是定义 LLM 驱动 Wiki 的结构、命名约定与工作流的配置文件。它类似于 [[entities/Claude-Code|Claude Code]] 中的 `CLAUDE.md` 或 Codex 中的 `AGENTS.md`——一份让大语言模型（LLM）理解如何摄取资料、回答询问以及执行维护操作的规则手册。Schema 使得 LLM 从一个通用聊天机器人转变为严格遵守规则的 Wiki 维护者。

在 [[concepts/LLM-Wiki|LLM-Wiki]] 的三层架构（原始资料层、Wiki 层、Schema 层）中，Schema 位于第三层，是保证多次会话之间输出一致、维护质量稳定的关键。

## 关键特征
- **规则定义文件**：包含页面结构模板、命名规范（如 slug 化规则）、分类标准（concept/entity 的 type/tags）、工作流指令等。
- **人机协同演化**：Schema 由用户与 LLM 共同维护，随领域需求和 Wiki 规模持续调整。
- **行为一致性**：每次操作（如 [[concepts/Ingest|Ingest]]、[[concepts/Query|Query]]）均基于 Schema 中记录的约定与偏好，无需每次重新说明规则。
- **三层架构的顶层**：位于原始资料（[[concepts/Raw-Sources|Raw-Sources]]）和 Wiki 层面之上，指导知识如何从原始资料流向结构化 Wiki。

## 应用
- **LLM Wiki 维护**：在 [[concepts/LLM-Wiki|LLM-Wiki]] 等系统中作为核心配置，确保 LLM 在创建、更新页面时格式统一、分类准确、链接正确。
- **跨会话质量保证**：通过预置的 [[concepts/Lint|Lint]] 规则（如非法标签检测、断链修复）自动维持 Wiki 健康度。
- **工作流自动化**：定义摄取、查询、合并等操作的完整流程，使 LLM 能在无人干预下自主执行维护任务。

## 相关概念
- [[concepts/Raw-Sources|Raw-Sources]]
- [[concepts/Ingest|Ingest]]
- [[concepts/Query|Query]]
- [[concepts/Lint|Lint]]

## 相关实体
暂无直接相关实体。

## 来源提及

- "The schema — a document (e.g. CLAUDE.md for Claude Code or AGENTS.md for Codex) that tells the LLM how the wiki is structured, what the conventions are, and what workflows to follow when ingesting sources, answering questions, or maintaining the wiki." (Schema——一份文档（例如Claude Code使用的CLAUDE.md或Codex使用的AGENTS.md），告诉LLM Wiki的结构、约定，以及在摄取资料、回答问题或维护Wiki时应遵循的工作流程。) — [[raw/Clippings/llm-wiki|llm-wiki]]