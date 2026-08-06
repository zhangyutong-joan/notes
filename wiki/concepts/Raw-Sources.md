---

type: concept
created: 2026-08-05
updated: 2026-08-05
sources: ["[[sources/llm-wiki_38393a]]"]
tags: [term]
aliases:
  - "原始资料"
  - "源文档集合"
  - "Raw Sources"
sources:
  - [[sources/llm-wiki_38393a]]
generation_complete: true
---


# Raw Sources

## 定义
在 LLM Wiki 架构中，**Raw Sources** 是用户精心整理并持久化存储的**原始文档层**。该层包含文章、论文、图片、数据文件等未经 LLM 修改的一手资料，作为整个 Wiki 系统不可动摇的**事实来源**。LLM 只能读取该层内容，无法对其进行任何修改，从而确保原始信息的完整性与可审计性。

## 关键特征
- **不可变性**：Raw Sources 层一旦写入即被锁定为只读状态，LLM 不具有写入、编辑或删除权限。
- **事实来源**：所有后续的 Wiki 页面（概念、实体等）均由该层的内容提取、推导而来，原始数据是唯一的权威依据。
- **与生成层分离**：Raw Sources 与 LLM 生成的 Wiki 内容在存储、访问、处理逻辑上彻底分离，两者互不污染。
- **可重新处理**：由于原始资料完整保留，用户可随时清空并重新触发 LLM 的摄取流程，生成全新的或修正后的 Wiki 视图，而无需担心原始数据丢失。
- **增量知识积累基石**：用户持续将新资料放入该层，驱动 LLM 进行分批摄取，实现基于证据的、持续扩展的知识库构建。

## 应用
- **知识库初始化**：用户将一组技术文档、论文或项目记录放入 Raw Sources，触发首次摄取生成基础 Wiki。
- **知识更新与修正**：当发现原始文档有误或需要补充新版本时，只需更新 Raw Sources 中的文件，重新处理即可同步 Wiki 内容。
- **混合来源验证**：结合多份原始资料交叉验证事实，提高 Wiki 知识的准确性和可靠性。
- **可审计性保障**：任何 Wiki 页面的论断都可以追溯回 Raw Sources 中的具体段落，便于人工审核与校正。

## 相关概念
- [[concepts/LLM-Wiki|LLM-Wiki]] — 整体框架，Raw Sources 是其不可缺失的数据基础层。
- [[concepts/Ingest|Ingest]] — 当用户向 Raw Sources 添加新资料时，触发 LLM 执行的摄取操作。
- [[concepts/Schema|Schema]] — 定义如何从 Raw Sources 中提取结构化信息的规则与模板。
- [[concepts/Index-and-Log|Index-and-Log]] — 记录每次摄取期间处理的原始资料及变更，用于管理 Raw Sources 的处理状态。

## 相关实体
暂无（该概念属于纯架构层，尚无直接绑定的具体实体）。

## 来源提及

- "Raw sources — your curated collection of source documents. Articles, papers, images, data files. These are immutable — the LLM reads from them but never modifies them. This is your source of truth." (原始资料——您精心整理的文件集合。包括文章、论文、图片和数据文件。这些是不可变的——LLM可以读取但不能修改。这是您的事实来源。) — [[raw/Clippings/llm-wiki|llm-wiki]]
- "You drop a new source into the raw collection and tell the LLM to process it." (您将新资料放入原始资料集合中，并告诉LLM处理它。) — [[raw/Clippings/llm-wiki|llm-wiki]]