---
type: source
created: 2026-08-05
updated: 2026-08-05
source_file: "[[raw/Clippings/llm-wiki.md]]"
tags: [clippings]
aliases: ["LLM Wiki 模式", "Karpathy LLM Wiki"]
contentHash: 2e72-08eca876
generation_complete: true
---

# LLM Wiki - Summary

## 来源
- Original file: [[raw/Clippings/llm-wiki.md]]
- Ingested: 2026-08-05

## 核心内容
本文提出了一种称为 [[concepts/LLM-Wiki|LLM Wiki]] 的个人知识管理新范式：让 LLM 从只读的[[concepts/Raw-Sources|原始源]]中提取信息，增量构建并维护一个结构化的 Markdown wiki，而非每次查询时重新检索。[[entities/Vannevar-Bush|Vannevar Bush]] 的 [[concepts/Memex|Memex]] 设想提供了历史渊源，但 LLM 解决了维护负担。架构分为三层，操作包括 [[concepts/Ingest|摄取]]、[[concepts/Query|查询]] 和 [[concepts/Lint|检查]]，由类似 [[concepts/CLAUDE-md|CLAUDE.md]] 的[[concepts/Schema|Schema]] 约束行为。[[concepts/Index-and-Log|index.md 和 log.md]] 负责导航与记录。与 [[concepts/RAG|RAG]] 相比，这种模式通过提前编译知识，避免了重复检索与推理，使知识库像代码库一样持续增长，人只需策展与提问。文中还推荐了 [[entities/Obsidian|Obsidian]]、[[entities/Marp|Marp]]、[[entities/qmd|qmd]] 等工具构成工作流。

## 关键实体
- [[entities/Obsidian|Obsidian]] — 作为 wiki 的可视化 IDE
- [[entities/Marp|Marp]] — 从 wiki 内容生成演示文稿的工具
- [[entities/qmd|qmd]] — 本地 Markdown 搜索引擎
- [[entities/Vannevar-Bush|Vannevar Bush]] — Memex 概念的提出者
- [[entities/Tolkien-Gateway|Tolkien Gateway]] — 粉丝维基，展示 wiki 的最终丰富程度
- [[entities/Obsidian-Web-Clipper|Obsidian Web Clipper]] — 快速将网页转为 Markdown 源
- [[entities/Dataview|Dataview]] — 对页面前置元数据进行查询的 Obsidian 插件

## 关键概念
- [[concepts/RAG|RAG]] — 传统的文档检索问答模式，缺乏知识积累
- [[concepts/LLM-Wiki|LLM Wiki]] — 由 LLM 增量构建的持久化知识库模式
- [[concepts/Memex|Memex]] — Vannevar Bush 的个人知识存储设想
- [[concepts/Index-and-Log|Index and Log]] — 以 index.md 和 log.md 维护导航与时间线
- [[concepts/CLAUDE-md|CLAUDE.md]] — Claude Code 中定义 wiki 结构和工作流的配置文件
- [[concepts/Raw-Sources|Raw Sources]] — 不可修改的原始文档层
- [[concepts/Ingest|Ingest]] — 将新源整合进 wiki 的核心操作
- [[concepts/Query|Query]] — 基于 wiki 的问答，结果可归档回 wiki
- [[concepts/Lint|Lint]] — 定期健康检查，消除矛盾与遗漏
- [[concepts/Schema|Schema]] — 指导 LLM 行为的总规则文件

## 要点
- LLM Wiki 是一种与 RAG 截然不同的知识管理范式：让 LLM 提前编译并维护一个持久化的 wiki，而非每次查询时重新检索。
- 架构分为三层：原始源（只读）、Wiki（LLM 维护的 Markdown 文件）和 Schema（指导 LLM 的规则文档，如 CLAUDE.md）。
- 三种核心操作：摄取（处理新源）、查询（基于 wiki 回答）、检查（定期健康检查，发现矛盾、孤立页面等）。
- index.md 和 log.md 分别提供内容目录和时间线，使 wiki 在中等规模下无需复杂搜索基础设施即可被高效导航。
- 工具链支持包括 Obsidian 作为可视化 IDE、Marp 生成演示、qmd 作为本地搜索引擎，以及 Dataview、Web Clipper 等。
- 模式的历史渊源可追溯到 Vannevar Bush 的 Memex，但 LLM 解决了维护负担问题，使个人知识库的持续增长成为可能。