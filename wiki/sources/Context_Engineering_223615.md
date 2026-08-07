---
type: source
created: 2026-08-06
updated: 2026-08-07
source_file: "[[raw/concept_note/Context_Engineering.md]]"
contentHash: 123c-1b13a176
generation_complete: true
sources:
  - "[[sources/上下文整理助手_bb5677]]"
tags:
  - "note"
aliases:
  - "上下文工程"
  - "CE"
---

# Context Engineering - 摘要

本文系统阐述了**上下文工程**的设计原则与常见误区，核心围绕 [[concepts/KV-Cache|KV Cache]] 和 [[concepts/Prompt-Cache|Prompt Cache]] 对前缀字节级稳定性的强制性要求。文中强调：[[concepts/System-Prompt|系统提示词]]、工具定义等前缀内容一旦确定就必须保持静态，动态信息只能追加到对话末尾，以避免缓存全面失效。常见的错误模式——[[concepts/动态系统提示词|动态系统提示词]]、[[concepts/Sliding-Window|滑动窗口]]——均因破坏前缀一致性而被反复警示。

文章进一步揭示了[[concepts/缓存一致性|缓存一致性]]如何反向主导 Agent 架构：[[concepts/缓存边界|缓存边界]]决定了提示词的排列顺序，子 Agent 必须与父 Agent 进行[[concepts/Sub-agent-alignment|字节级对齐]]。在提示工程层面，讨论了语气、结构化、流程驱动 SOP、业务规则细化以及 [[concepts/Few-shot-示例|Few-shot 示例]] 的嵌入技巧。最后介绍了 [[concepts/Agent-Skills|Agent Skills]] 与[[concepts/渐进式披露|渐进式披露]]的按需加载机制，以及以[[concepts/来源标记|来源标记]]和[[concepts/结构化角色|结构化角色]]为核心的[[concepts/Prompt-Injection|提示注入]]防御体系。

## 关键实体
（本文未提取独立实体）

## 关键概念
- [[concepts/KV-Cache|KV Cache]]
- [[concepts/Prompt-Cache|Prompt Cache]]
- [[concepts/Chat-Template|Chat Template]]
- [[concepts/In-Context-Learning|In-Context Learning]]
- [[concepts/System-Prompt|System Prompt]]
- [[concepts/Prompt-Injection|Prompt Injection]]
- [[concepts/Sliding-Window|滑动窗口]]
- [[concepts/Agent-Skills|Agent Skills]]
- [[concepts/缓存一致性|缓存一致性]]
- [[concepts/Few-shot-示例|Few-shot 示例]]
- [[concepts/动态系统提示词|动态系统提示词]]
- [[concepts/渐进式披露|渐进式披露]]
- [[concepts/SKILL-md|SKILL.md]]
- [[concepts/YAML-frontmatter|YAML frontmatter]]
- [[concepts/来源标记|来源标记]]
- [[concepts/结构化角色|结构化角色]]
- [[concepts/输入清洗|输入清洗]]
- [[concepts/Sub-agent-alignment|Sub-agent alignment]]
- [[concepts/缓存边界|缓存边界]]

## 要点
- KV Cache 与 Prompt Cache 均要求前缀字节级稳定，任何修改都会导致缓存失效。
- 系统提示词、工具定义应置于前缀并永不修改，动态信息追加入对话末尾。
- 常见反模式：动态系统提示词、滑动窗口，会破坏缓存一致性、丢失关键信息。
- 缓存边界决定提示词排列——经济性优先于语义逻辑。
- 系统提示词的优化涵盖语气、结构化（XML/Markdown）、流程驱动、Few-shot 示例等。
- Agent Skills 采用渐进式披露：静态前缀仅保存元数据，完整 Schema 按需加载，维持缓存并降低 token 开销。
- 缓存一致性主导 Agent 架构：子 Agent 必须与父 Agent 字节对齐，工具结果替换字符串在首次生成后冻结。
- 防御提示注入：来源标记、严格使用 Chat Template 角色体系、输入清洗。