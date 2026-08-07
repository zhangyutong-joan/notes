---

type: concept
created: 2026-08-06
updated: 2026-08-06
sources: ["[[sources/Context_Engineering_223615]]"]
tags: [term]
aliases:
  - "系统提示词"
  - "System Prompt"
sources:
  - [[sources/Context_Engineering_223615]]
generation_complete: true
---


# System Prompt

## 定义
System Prompt（系统提示词）是提示工程中最重要的结构化组件，用于在对话开始时向大语言模型（LLM）声明其身份、行为准则、约束条件、输出格式与工作流程。系统提示词通常被置于整个上下文的最前端，与工具定义等静态内容一同构成 **KV Cache** 和 **Prompt Cache** 的可缓存前缀，从而在多次推理中复用而无需重复计算。

## 关键特征
- **静态前缀定位**：系统提示词固定于 token 序列的开头，与工具定义共同组成模型请求中的静态前缀，直接影响缓存策略与推理效率
- **缓存亲和性**：由于系统提示词一旦确定就绝不应被修改，否则会导致已经构建的 KV Cache 和 Prompt Cache 全面失效，引发额外的计算开销和延迟
- **动态信息分离**：需要随用户请求变化的上下文（如当天日期、实时数据）不应写入系统提示词，而应以用户消息的形式追加到序列末尾，保护静态缓存的完整性
- **结构化与风格优化**：通过使用 XML、Markdown 等结构化标记、设定语气风格（如正式、简洁）、嵌入流程驱动的 SOP 式描述以及 Few-shot 示例，在清晰的行为框架内最大化模型的认知资源利用
- **安全与对齐**：系统提示词也用于设定安全护栏，例如防止越狱、明确拒绝范围、强调合规性等，是实现模型对齐的重要手段

## 应用
- **Agent 行为定义**：在 [[entities/WikiLLM|WikiLLM]]、[[entities/Claude-Code|Claude-Code]] 等应用中，通过系统提示词定义 Agent 的角色、可用工具集和交互协议
- **提示缓存优化**：利用系统提示词作为静态前缀的特性，配合 [[concepts/KV-Cache|KV-Cache]] 和 [[concepts/Prompt-Cache|Prompt-Cache]] 技术，显著降低多次推理的延迟和计算成本
- **Few-shot 引导**：将 [[concepts/few-shot|Few-shot 示例]] 嵌入系统提示词，为模型提供任务格式和风格参照，提升少样本场景下的回答质量
- **动态信息隔离**：将实时性内容（如用户查询、检索结果）留给用户消息部分，确保系统提示词层的缓存可复用性，这一架构在 [[concepts/dynamic-system-prompt|动态系统提示词]] 设计中得到贯彻
- **安全防护**：通过系统提示词引入防注入规则，抵御 [[concepts/prompt-injection|提示注入]] 攻击，并定义敏感话题的处理边界

## 相关概念
- [[concepts/prompt-engineering|提示工程]]
- [[concepts/KV-Cache|KV-Cache]]
- [[concepts/Prompt-Cache|Prompt-Cache]]
- [[concepts/prompt-injection|提示注入]]
- [[concepts/few-shot|Few-shot 示例]]
- [[concepts/dynamic-system-prompt|动态系统提示词]]
- [[concepts/Chat-Template|Chat-Template]]

## 相关实体
- [[entities/WikiLLM|WikiLLM]]
- [[entities/Claude-Code|Claude-Code]]

## 来源提及

- "提示工程（Prompt Engineering）的核心对象是系统提示词（System Prompt）。系统提示词定义了 Agent 的身份、行为规则、约束条件和工作流程。" (提示工程（Prompt Engineering）的核心对象是系统提示词（System Prompt）。系统提示词定义了 Agent 的身份、行为规则、约束条件和工作流程。) — [[raw/concept_note/Context_Engineering|Context_Engineering]]