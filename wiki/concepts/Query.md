---

type: concept
created: 2026-08-05
updated: 2026-08-05
sources: ["[[sources/llm-wiki_38393a]]"]
tags: [method]
aliases:
  - "查询操作"
  - "Wiki查询"
  - "Query操作"
sources:
  - [[sources/llm-wiki_38393a]]
generation_complete: true
---


# Query

## 定义
Query（查询）是 LLM 在 Wiki 上触发的一次智能问答操作。用户提出问题后，LLM 会搜索相关页面、深读内容，并综合多个来源生成带有引用的回答。回答可以采用 Markdown 页面、对比表格、幻灯片、图表或画布等多种形式。Query 操作的核心洞见在于：优秀的问答结果可以作为新页面归档回 Wiki，将临时探索转化为永久知识资产，形成与资料摄取（Ingest）类似的累积效应。

## 关键特征
- 跨页面综合：自动定位并阅读多个相关页面，融合不同来源的信息，生成高质量、有引用的回答。
- 多形态输出：支持产生 Markdown 页面、对比表格、幻灯片、图表、画布等多种格式，适配不同场景的表达需求。
- 闭环知识积累：生成的优秀回答可以被归档为新的 Wiki 页面，使问答成果永久沉淀，实现从“问答”到“建库”的转变。
- 依赖交叉链接结构：充分利用 Wiki 内部页面间的超链接关系，快速发现与问题相关的知识网络。
- 与 Ingest、Lint 并列的核心操作：Query、Ingest、Lint 三者共同构成 LLM Wiki 的三大基础操作循环。

## 应用
- **复杂问题综合**：当问题需要跨多个概念或实体进行综合时，Query 能自动聚合分散在多个页面中的信息，提供整体视角。
- **临时探索转永久知识**：用户在交流过程中的探索性提问，一旦生成有价值的回答，可立即固化为页面，避免知识流失。
- **知识发现与关联**：借助 Wiki 的链接结构，Query 不仅回答当前问题，还能揭示原本未注意到的概念关系。
- **文档与报告生成**：直接通过自然语言提问，快速生成结构化的对比表格、演讲稿（幻灯片）或示意图，用于分享与复盘。

## 相关概念
- [[concepts/Ingest|Ingest]]
- [[concepts/Lint|Lint]]
- [[concepts/Schema|Schema]]
- [[concepts/LLM-Wiki|LLM-Wiki]]
- [[concepts/斜杠命令|斜杠命令]]
- [[concepts/Index-and-Log|Index-and-Log]]

## 相关实体
暂无

## 来源提及

- "Query. You ask questions against the wiki. The LLM searches for relevant pages, reads them, and synthesizes an answer with citations. Answers can take different forms depending on the question — a markdown page, a comparison table, a slide deck (Marp), a chart (matplotlib), a canvas. The important insight: good answers can be filed back into the wiki as new pages...." (查询。您针对Wiki提出问题。LLM搜索相关页面，阅读它们，并综合给出带引用的答案。答案可根据问题的不同以多种形式呈现——Markdown页面、对比表格、幻灯片（Marp）、图表（matplotlib）、画布。重要的是：好的答案可以作为新页面归档回Wiki中。) — [[raw/Clippings/llm-wiki|llm-wiki]]