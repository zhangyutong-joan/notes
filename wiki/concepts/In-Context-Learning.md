---

type: concept
created: 2026-08-06
updated: 2026-08-06
sources: ["[[sources/Context_Engineering_223615]]"]
tags: [theory]
aliases:
  - "上下文学习"
  - "ICL"
  - "In-Context Learning"
sources:
  - [[sources/Context_Engineering_223615]]
generation_complete: true
---


# In-Context Learning

## 定义
In-Context Learning（上下文学习）是指大语言模型在**不更新自身参数**的条件下，仅通过当前输入中提供的自然语言指令及少量示例（demonstrations）即可临时、有效地适应新任务的能力。这种能力完全来源于模型在预训练阶段习得的模式匹配与推理机制，无需任何梯度计算或微调。

## 关键特征
- **无参数更新**：模型权重全程冻结，所有学习信号均隐含在输入的上下文窗口内。
- **强依赖底层能力**：模型的“长思维链推理”和“工具调用”等高级行为严重依赖成熟的 In-Context Learning 能力，否则无法从示例中正确抽象出任务模式。
- **对示例格式敏感**：Few-shot 示例是典型的应用方式，少量精选示例的指导效果往往优于等量篇幅的抽象规则描述。
- **位置影响缓存**：在上下文工程设计（如 Prompt Caching）中，示例所放置的静态前缀应保持字节级不变，否则可能破坏缓存命中，影响推理性能。
- **临时性**：学习到的行为仅在当前会话或输入上下文中有效，不改变模型本身，对话结束即“遗忘”。

## 应用
- **提示工程（[[concepts/提示工程|提示工程]]）**：通过在系统提示词中嵌入 Few-shot 示例，使模型快速“学会”特定的输出格式、判断逻辑或工具调用模式，无需训练。
- **Agent Skills 设计（[[concepts/Agent-Skills|Agent Skills]]）**：在智能体框架中，利用 In-Context Learning 为模型动态注入新技能或工作流，使同一基础模型在运行时具备多样化能力。
- **缓存友好部署**：结合 [[concepts/KV-Cache|KV-Cache]] 和 [[concepts/Prompt-Cache|Prompt-Cache]] 技术，将不变的指令-示例前缀固化，降低每次请求的推理成本。

## 相关概念
- [[concepts/Few-shot-示例|Few-shot 示例]]
- [[concepts/提示工程|提示工程]]
- [[concepts/Agent-Skills|Agent Skills]]
- [[concepts/KV-Cache|KV-Cache]]
- [[concepts/Prompt-Cache|Prompt-Cache]]

## 相关实体
暂无直接关联的特定实体。该能力内嵌于大语言模型本身，属于模型行为层面的理论概念。

## 来源提及

- "模型的长思维链能力和工具调用能力都对上下文学习（In-Context Learning）能力有很强的依赖——所谓上下文学习，是指模型不需要重新训练，仅凭输入中给出的指令和示例就能适应新任务的能力。" (模型的长思维链能力和工具调用能力都对上下文学习（In-Context Learning）能力有很强的依赖——所谓上下文学习，是指模型不需要重新训练，仅凭输入中给出的指令和示例就能适应新任务的能力。) — [[raw/concept_note/Context_Engineering|Context_Engineering]]