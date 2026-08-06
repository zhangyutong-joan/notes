---

type: concept
created: 2026-08-05
updated: 2026-08-05
sources: ["[[sources/llm-wiki_38393a]]"]
tags: [method]
aliases:
  - "wiki indexing and logging"
  - "index and log"
  - "索引和日志"
sources:
  - [[sources/llm-wiki_38393a]]
generation_complete: true
---


# Index and Log

## 定义
Index and Log（索引与日志）是 LLM Wiki 知识库架构中的两个核心维护文件：**index.md** 作为按分类层级组织的目录索引，列出所有 wiki 页面的链接及简要描述；**log.md** 是以时间顺序追加的操作记录，每条记录包含摄取、查询、检查等事件的元数据。两者共同支撑 wiki 的浏览、追溯和轻量级查询，无需引入独立数据库或复杂检索基础设施。

## 关键特征
- **轻量目录结构**：`index.md` 按实体/概念/源等类别分块，每个条目仅含页面链接和一行描述，LLM 可通过单次读取快速定位目标页面。
- **自动化同步**：每次新内容摄取（ingest）时，LLM 自动更新 `index.md`，确保目录与最新知识图谱一致。
- **操作可追溯**：`log.md` 以追加行记录每次操作的时间、类型、涉及文件及结果，形成 wiki 演化时间线。
- **工具友好**：日志文件采用纯文本 + 固定字段格式，兼容 `grep`/`awk` 等命令行工具进行快速检索和统计。
- **去基础设施化**：省去向量数据库或全文检索引擎，所有检索仅依赖文件系统读取，符合“简单优先”的设计哲学。

## 应用
- 在 [[concepts/LLM-Wiki|LLM Wiki]] 项目中，`index.md` 是 LLM 回答用户查询时的第一关：先读索引获得候选页面，再读取具体页面内容以生成答案。
- `log.md` 用于审计和调试，检查 wiki 过去几次操作、识别异常摄取，或分析 wiki 知识增长曲线。
- 二者结合可实现简单的“Time Travel”——通过日志定位某次操作前的状态，再根据索引查看对应版本的页面快照。

## 相关概念
- [[concepts/LLM-Wiki|LLM-Wiki]] — 索引与日志是该架构的组成部分
- [[concepts/最小闭环|最小闭环]] — 索引-日志机制体现了“读取 → 更新 → 记录”的最小可行循环
- [[concepts/防呆|防呆]] — 索引自动更新和日志追加的设计减少了人为遗漏，属于防错策略

## 相关实体
暂无直接关联实体。

## Mentions in Source
*无原始引用，本页为归纳性概念页面。*

## 来源提及

- "index.md is content-oriented. It's a catalog of everything in the wiki — each page listed with a link, a one-line summary, and optionally metadata like date or source count. Organized by category (entities, concepts, sources, etc.). The LLM updates it on every ingest." (index.md 是内容导向的。它是 wiki 中所有内容的目录——每个页面都带有链接、一行摘要，以及可选的元数据，如日期或来源数量。按类别组织（实体、概念、来源等）。LLM 在每次摄取时更新它。) — [[raw/Clippings/llm-wiki|llm-wiki]]