---

type: concept
created: 2026-08-05
updated: 2026-08-05
sources: ["[[sources/llm-wiki_38393a]]"]
tags: [method]
aliases:
  - "LLM-maintained wiki"
  - "persistent wiki building"
sources:
  - [[sources/llm-wiki_38393a]]
generation_complete: true
---


# LLM Wiki

## 定义
LLM Wiki 是由 [[entities/Andrej-Karpathy|Andrej-Karpathy]] 提出的一种知识管理范式，旨在通过大型语言模型（LLM）增量式地构建并维护一个持久化的结构化知识库。与传统 RAG 不同，LLM Wiki 强调从原始源中提取信息，整理成带有交叉引用的 Markdown 页面（实体页、概念页、摘要等），形成一个可编译、可持续演进的复合人工制品，使知识像代码库一样增长和迭代。

## 关键特征
- **持久化、复合的知识库**：知识以 Markdown Wiki 形式存在，编译一次并可反复查询、更新，而不是每次运行时临时检索。
- **三层架构**：底层为原始源（文档、对话等），中间层为结构化 Wiki 页面，顶层为定义结构的 Schema（如实体类型、概念类型、命名规范）。
- **三大核心操作**：摄取（从源中提取事实并创建/更新页面）、查询（基于 Wiki 回答问题或生成报告）、检查（验证一致性、查缺补漏）。
- **脱离实时检索**：不依赖文档分块与向量召回，知识在编译阶段已完成整合，查询时直接利用结构化的语义网络。
- **人类策展角色**：人的职责是设定方向、审核内容、修正错误，而非手工编写每一个页面。
- **代码化知识演进**：Wiki 通过版本控制（如 Git）管理，变更可追溯、可回滚，类比软件开发流程。

## 应用
- **个人知识管理**：构建跨领域的长期记忆库，自动将学习笔记、文章摘要转化为结构化 wiki。
- **项目文档**：为软件项目维护一致、可自动更新的技术文档，保持与代码库同步。
- **研究辅助**：聚合论文、实验记录，形成可交互的领域知识图谱，加速文献综述。
- **企业知识库**：从内部文档、会议记录中持续提取流程与规范，降低知识流失风险。
- **教育场景**：将课程材料转化为超链接密集的百科式教材，支持智能问答与追溯。

## 相关概念
- [[concepts/RAG|RAG]] — 检索增强生成，LLM Wiki 的对照范式，强调实时检索而非预先编译
- [[concepts/Memex|Memex]] — Vannevar Bush 构想的个人记忆扩展机器，LLM Wiki 可视为其现代实现
- [[concepts/Index-and-Log|Index and Log]] — 一种结构化日志与索引的知识组织思想，与 Wiki 架构相互呼应

## 相关实体
- [[entities/Andrej-Karpathy|Andrej-Karpathy]] — 提出者，阐述了 LLM Wiki 的核心思想
- [[entities/Obsidian|Obsidian]] — 常用于构建本地 Markdown Wiki 的工具，契合持久化理念
- [[entities/qmd|qmd]] — 支持可执行文档的格式，利于自动生成与更新 Wiki 内容
- [[entities/Tolkien-Gateway|Tolkien-Gateway]] — 大规模主题 Wiki 实例，展示了结构化知识库的形态
- [[entities/WikiLLM|WikiLLM]] — 相关项目，探索 LLM 与 Wiki 构建的结合

## 来源提及

- "The idea here is different. Instead of just retrieving from raw documents at query time, the LLM incrementally builds and maintains a persistent wiki — a structured, interlinked collection of markdown files that sits between you and the raw sources." (这里的想法不同。不是在查询时从原始文档检索，LLM 增量构建和维护一个持久化的 wiki——一个结构化的、相互链接的 Markdown 文件集合，位于你和原始源之间。) — [[raw/Clippings/llm-wiki|llm-wiki]]