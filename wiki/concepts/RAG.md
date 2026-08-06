---

type: concept
created: 2026-08-05
updated: 2026-08-05
sources: []
tags: [method]
aliases:
  - "Retrieval-Augmented Generation"
  - "检索增强生成"
sources:
  - [[sources/llm-wiki_38393a]]
generation_complete: true
---


# RAG

## 定义
RAG（检索增强生成）是一种通用的大语言模型（LLM）使用模式：用户上传文档集合，系统在收到查询时从集合中检索相关片段，并将这些片段作为上下文提供给 LLM，以生成更准确、有依据的答案。该方法本质上是一种“查询时检索”范式，每次新问题都需要重新搜索文档库。

## 关键特征
- **查询驱动检索**：仅在用户提问时触发检索，不建立长期、结构化的知识索引。
- **无状态性**：每次查询相互独立，回答完成后不保留任何新的知识表示或推理成果。
- **碎片化**：答案基于离散的文档片段拼接，缺乏对文档整体的统一理解。
- **知识未固化**：反复出现的关联和洞察不会被沉淀下来，系统无法从历史查询中学习。
- **跨文档困难**：当问题需要综合多篇文档时，模型必须反复定位、比对和拼接信息。

## 应用
- 企业知识库问答（如员工手册、规范查询）
- 客户支持系统（产品文档自动应答）
- 研究辅助（论文集合的摘要式提问）
- 法律、医疗等领域的资料检索与解释
- 私人文档助手（如笔记、日记的语义搜索与回答）

## 相关概念
- [[concepts/llm-wiki|LLM Wiki]] — 作为 RAG 的替代方案，通过预先将文档知识编译为结构化 wiki 来避免重复检索与碎片化推理。

## 相关实体
暂无直接关联实体。

## Mentions in Source
暂无引用来源。

## 来源提及

- "Most people's experience with LLMs and documents looks like RAG: you upload a collection of files, the LLM retrieves relevant chunks at query time, and generates an answer. This works, but the LLM is rediscovering knowledge from scratch on every question. There's no accumulation." (大多数人使用 LLM 与文档交互的体验类似于 RAG：上传一组文件，LLM 在查询时检索相关片段并生成答案。这可以工作，但 LLM 在每次提问时都从头重新发现知识。没有任何积累。) — [[raw/Clippings/llm-wiki|llm-wiki]]