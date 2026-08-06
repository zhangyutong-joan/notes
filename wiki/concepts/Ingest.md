---

type: concept
created: 2026-08-05
updated: 2026-08-05
sources: ["[[sources/llm-wiki_38393a]]"]
tags: [method]
aliases:
  - "摄取操作"
  - "资料摄取"
  - "Ingest"
sources:
  - [[sources/llm-wiki_38393a]]
generation_complete: true
---


# Ingest

## 定义
Ingest 是 [[concepts/LLM-Wiki|LLM Wiki]] 的核心操作之一，指将新的原始资料读入并持续整合到结构化 Wiki 中的完整过程。用户将资料放入 [[concepts/Raw-Sources|Raw Sources]] 后，LLM 会阅读内容、与用户讨论要点，然后自动或半自动地创建摘要页面、更新索引与日志（[[concepts/Index-and-Log|Index and Log]]），并修改全 Wiki 范围内所有关联的实体和概念页面，使新知识融入现有知识结构而非成为孤岛。

## 关键特征
- 增量式知识积累：每一次摄取都是对现有 Wiki 的增量增强，新资料被分解、链接并嵌入已有词条网络
- 高页面覆盖率：一次完整的摄取可能涉及 10 到 15 个页面的创建或更新，包括摘要页、实体/概念页、索引和日志
- 用户参与灵活度：支持“逐份摄入并保持参与”模式（用户全程审查与讨论），也支持“批量摄入但监督较少”模式
- 工作流可定义：具体的摄取步骤和规则在 [[concepts/Schema|Schema]] 中根据用户偏好定义并演进，使摄取行为可定制、可复用
- 与查询和纠错协同：摄取后可通过 [[concepts/Query|Query]] 操作检索新增的结构化知识，通过 [[concepts/Lint|Lint]] 操作检查和修复链接一致性

## 应用
- 构建个人或项目持续更新的知识库：将遇到的新文档、文章、笔记等持续转化为互联的结构化知识
- 研究追踪：对一系列论文、技术文档进行增量摄取，形成领域知识图谱
- 团队知识管理：以规范化流程将会议记录、设计文档等实时整合到共享 Wiki 中

## 相关概念
- [[concepts/Raw-Sources|Raw Sources]]
- [[concepts/Schema|Schema]]
- [[concepts/Query|Query]]
- [[concepts/Lint|Lint]]
- [[concepts/LLM-Wiki|LLM Wiki]]
- [[concepts/Index-and-Log|Index and Log]]

## 相关实体
（暂无直接关联的实体）

## 来源提及

- "Ingest. You drop a new source into the raw collection and tell the LLM to process it. An example flow: the LLM reads the source, discusses key takeaways with you, writes a summary page in the wiki, updates the index, updates relevant entity and concept pages across the wiki, and appends an entry to the log. A single source might touch 10-15 wiki pages...." (摄取。您将新资料放入原始集合中，并告诉LLM进行处理。一个典型流程是：LLM阅读资料，与您讨论关键要点，在Wiki中撰写摘要页面，更新索引，更新整个Wiki中相关的实体和概念页面，并追加一条日志记录。一份资料可能涉及10-15个Wiki页面。) — [[raw/Clippings/llm-wiki|llm-wiki]]