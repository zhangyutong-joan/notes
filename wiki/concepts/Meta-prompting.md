---

type: concept
created: 2026-08-07
updated: 2026-08-07
sources: ["[[sources/notes_795b78]]"]
tags: [method]
aliases:
  - "元提示"
  - "Meta-prompting"
  - "元提示技术"
sources:
  - [[sources/notes_795b78]]
generation_complete: true
---


# Meta-prompting

## 定义
Meta-prompting 是一种利用提示词来优化提示词的技术。用户提供一个“元提示”，指示大语言模型对原始提示进行改写、扩展或校准，从而获得更高质量的输出。该方法将提示工程的部分劳动自动化，借助模型对语言的深刻理解，实现比人工手动调优更精细的调整。

## 关键特征
- **以提示调优提示**：核心机制是通过 LLM 本身来评估和改进输入的提示词，形成“提示对提示”的闭环。
- **自动化提示工程**：将反复试错、手工修正的提示优化过程部分自动化，降低人工调试成本。
- **提升输出质量**：元提示能引导模型对原始指令进行润色、补充上下文或消除歧义，从而生成更准确、更符合期望的回应。
- **模型自优化**：利用了 LLM 在语言理解和生成方面的强项，让模型“自我反思”并改进任务描述。

## 应用
- **自动提示优化流水线**：在复杂 AI 对话系统中，可将 meta-prompting 作为预处理步骤，持续提升用户提示的质量。
- **低质量输入的增强**：当面对含糊、不完整或非专业的用户查询时，元提示可引导模型自动补全、规范或澄清问题。
- **教育与学习材料生成**：用于自动改写或扩写教学提示，使 AI 辅助的教学内容生成更可控、更精准。
- **提示工程辅助工具**：为开发者提供快速原型和提示词版本迭代的自动化手段，例如 OpenAI Cookbook 中的 `Enhance_your_prompts_with_meta_prompting` 示例。

## 相关概念
暂无直接关联的概念页面。

## 相关实体
- [[entities/Enhance_your_prompts_with_meta_prompting|Enhance_your_prompts_with_meta_prompting]]：OpenAI Cookbook 中具体展示 meta-prompting 过程的示例项目。

## 来源提及

- "[Enhance_your_prompts_with_meta_prompting](https://github.com/openai/openai-cookbook/blob/main/examples/Enhance_your_prompts_with_meta_prompting.ipynb)" (元提示优化项目（GitHub）) — [[raw/prompt_pool/notes|notes]]
- "来自openai-cookbook/examples /Enhance_your_prompts_with_meta_prompting.ipynb" (来自 OpenAI Cookbook 的元提示示例) — [[raw/prompt_pool/notes|notes]]