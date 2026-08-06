---

type: entity
created: 2026-08-05
updated: 2026-08-05
sources: ["[[sources/llm-wiki_38393a]]"]
tags: [product]
aliases:
  - "qmd"
sources:
  - [[sources/llm-wiki_38393a]]
generation_complete: true
---


# qmd

## 描述
qmd 是一个本地 Markdown 搜索引擎，专为[[concepts/llm-wiki|LLM Wiki]]设计。它通过 BM25 与向量搜索的混合策略进行高效检索，并在本机利用 LLM 对结果进行重排序，无需外部服务。当[[concepts/index-and-log|Index and Log]]中的简单索引（如 index.md）无法满足大规模 wiki 的搜索需求时，qmd 成为推荐的替代工具。它提供了命令行接口（CLI）供 LLM 直接调用，还支持 MCP 服务器，允许 LLM 将其作为原生工具使用，从而在 wiki 中快速定位相关页面。

## 相关实体
暂无

## 相关概念
- [[concepts/llm-wiki|LLM Wiki]]
- [[concepts/index-and-log|Index and Log]]

## 来源提及

- "qmd is a good option: it's a local search engine for markdown files with hybrid BM25/vector search and LLM re-ranking, all on-device. It has both a CLI (so the LLM can shell out to it) and an MCP server (so the LLM can use it as a native tool)." (qmd 是一个不错的选择：它是一个本地 Markdown 文件搜索引擎，具有混合 BM25/向量搜索和 LLM 重排序功能，全部在设备上运行。它既有一个 CLI（因此 LLM 可以将其作为 shell 命令调用），又有一个 MCP 服务器（因此 LLM 可以将其用作原生工具）。) — [[raw/Clippings/llm-wiki|llm-wiki]]