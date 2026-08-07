---

type: concept
created: 2026-08-06
updated: 2026-08-06
sources: ["[[sources/Context_Engineering_223615]]"]
tags: [method]
aliases:
  - "少样本示例"
sources:
  - [[sources/Context_Engineering_223615]]
generation_complete: true
---


# Few-shot 示例

## 定义
Few-shot 示例是一种在大型语言模型的系统提示词中预先嵌入少量任务范例的做法。它利用模型的 In‑Context Learning 能力，使模型在推理时通过观察示例临时学会任务模式，而不依赖权重更新。在实际应用中，几个精心挑选的示例往往比冗长的抽象规则描述更能准确引导模型输出。

## 关键特征
- 嵌入位置固定：示例被建议放入系统提示词（[[concepts/System-Prompt|System Prompt]]），成为静态前缀的一部分。
- 对 KV 缓存敏感：由于系统前缀的字节级稳定性直接影响 [[concepts/KV-Cache|KV Cache]] 的复用效率，Few-shot 示例一旦确定就需要保持不变。
- 数量控制：通常放置两到三个示例即可达到理想效果，较多示例会额外消耗 token 且收益递减。
- 与规则互补：虽然示例属于提示工程，但它与工具定义等静态提示一起，构成了优化系统提示词的一个维度，并能与缓存边界协调。
- 本质是 [[concepts/In-Context-Learning|In-Context Learning]] 的具体应用，不需要模型参数更新。

## 应用
- 文本分类：用 2–3 个标注样本告诉模型类别模式。
- 翻译任务：给出源语言-目标语言对，让模型理解风格和术语。
- 代码生成：展示期望的代码格式、注释风格和解决方案逻辑。
- 对话式 AI 对齐：通过示例对话规范助手的语气、边界和任务流程。
- 与 Prompt Cache 协同：在 [[concepts/Prompt-Cache|Prompt Cache]] 设计中，固定示例可被安全预计算并缓存，降低首 token 延迟。

## 相关概念
- [[concepts/In-Context-Learning|In-Context Learning]]
- [[concepts/System-Prompt|System Prompt]]
- [[concepts/KV-Cache|KV Cache]]
- [[concepts/Prompt-Cache|Prompt Cache]]（间接相关）

## 相关实体
暂无特定实体直接关联。

## 来源提及

- "Few-shot 示例：模型的上下文学习能力会从示例中“临时学会”这些模式，其效果往往胜过等量篇幅的抽象规则。" (Few-shot 示例：模型的上下文学习能力会从示例中“临时学会”这些模式，其效果往往胜过等量篇幅的抽象规则。) — [[raw/concept_note/Context_Engineering|Context_Engineering]]