---
type: concept
created: 2026-08-07
updated: 2026-08-07
generation_complete: true
sources:
  - "[[sources/上下文整理助手_bb5677]]"
  - "[[sources/notes_795b78]]"
tags:
  - "term"
aliases:
  - "参考材料"
  - "参考文献"
  - "References"
---

# References

## 定义
References 指单次任务需要参考的外部材料，如图像、设计文件、文档或代码片段。这些材料为 Agent 提供执行任务所需的背景和数据，是任务级上下文的一部分。上下文整理助手最终需输出本次任务应提供的 References 清单，以帮助 Agent 获取必要的上下文。该概念体现了上下文工程中「按需提供参考」的思想，避免无关信息的干扰。

## 关键特征
- 属于任务级上下文，与单次任务绑定，而非持久记忆或系统设定
- 形式多样：可以是图像、设计文件、文档、代码片段、网页链接等
- 按需供给：只提供与当前任务直接相关的材料，避免信息过载和上下文窗口浪费
- 在上下文整理流程中，作为上下文整理助手的输出内容之一，指导 Agent 获取必要的外部数据
- 在分层设计中，References 帮助 Agent 区分“参考什么”和“我要做什么”，从而提升任务处理质量；其核心价值在于将一次性参考资料与项目约定、技能流程分离，是构建精细化 Agent 上下文的关键组件
## 应用
- 在提示工程中，用于向 LLM Agent 提供具体任务的背景材料，提升任务完成质量和准确性
- 在上下文整理助手（COA）的工作流中，作为分析后生成的推荐清单，帮助用户准备所需的上下文
- 适用于需要外部知识或参考资料的编程、设计、写作等复杂任务场景

## 相关概念
- [[concepts/上下文工程|上下文工程]]：References 是上下文工程中任务级上下文的具体实现与载体
- [[concepts/上下文整理助手|上下文整理助手]]：负责分析任务需求并输出 References 清单的核心组件
- [[concepts/Your-prompt|Your prompt]]：References 所依附的任务说明部分，两者共同构成完整的任务指示
- [[concepts/Claude Agent上下文结构|Claude Agent上下文结构]]：定义 References 所在整体上下文分层框架的顶层概念
## 相关实体
无特定相关实体。

## 来源提及

- "2. References：这次任务需要参考哪些材料（如截图、设计稿、文档、代码文件）" — [[raw/prompt_pool/notes|notes]]
- "3. 本次任务应该作为 References 提供的材料清单" — [[raw/prompt_pool/notes|notes]]
- "**References：** 告诉 Agent 这次任务参考哪些具体材料，可以是 specs、mockups、code、HTML artifact；" (**参考资料：** 告诉 Agent 这次任务参考哪些具体材料，可以是规格说明、原型、代码、HTML 产出物；) — [[raw/prompt_pool/notes|notes]]