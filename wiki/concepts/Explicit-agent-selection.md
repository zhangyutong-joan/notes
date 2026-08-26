---

type: concept
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [method]
aliases:
  - "agent selection"
  - "Arm 2"
  - "Explicit skill selection"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Explicit agent selection

## 定义

Explicit agent selection 是论文 RQ4 中的第二个离线诊断实验（Arm 2），旨在将技能选择与后续执行失败解耦。在该实验中，每个任务向代理呈现一个可用技能候选池，代理必须明确选择其认为有用的技能，但不执行下游任务。该方法用于评估代理能否仅凭任务上下文和技能描述识别有用技能，避免将选择能力与执行能力混为一谈。

## 关键特征

- **离线诊断实验设计**：作为 RQ4 的 Arm 2，与 embedding-based retrieval 和真实执行实验并列，用于隔离技能选择环节
- **选择与执行解耦**：代理只做技能选择，不执行下游任务，从而将"能否选对技能"与"能否用好技能"分离
- **基于上下文与描述的选择**：代理仅依赖任务上下文和技能描述做出选择，不涉及实际调用或执行反馈
- **双模型配对**：实验使用 [[entities/Gemini-CLI|Gemini CLI]] + [[entities/Gemini-3-1-Pro-Preview|Gemini-3.1-Pro-Preview]] 和 [[entities/Codex|Codex]] + [[entities/GPT-5-4|GPT-5-4]] 两种代理-模型组合
- **选择精确率高于实际使用精确率**：结果显示代理的选择精确率高于执行时的实际使用精确率，说明选择能力与执行效果之间存在落差
- **语义混淆放大选择难度**：在相似干扰项条件下选择难度显著增加，表明语义混淆是影响技能识别的重要因素
- **揭示可用性与使用之间的差距**：与 embedding-based retrieval 和真实执行共同揭示技能可用性与技能使用之间的差距

## 应用

- **技能识别能力评估**：用于单独衡量代理在给定候选池中识别有用技能的能力，而非端到端执行能力
- **失败归因分析**：通过解耦选择与执行，帮助区分代理失败源于技能选择错误还是技能执行偏差
- **技能池质量诊断**：与 [[concepts/Skill-pool-construction|Skill pool construction]] 配合，评估候选技能池的构建是否便于代理做出正确选择
- **语义干扰研究**：利用相似干扰项设计，量化 [[concepts/Semantic-confusability|Semantic confusability]] 对代理技能识别的影响

## 相关概念

- [[concepts/Embedding-based-retrieval|Embedding-based retrieval]]
- [[concepts/Retrieval-bottleneck|Retrieval bottleneck]]
- [[concepts/Semantic-confusability|Semantic confusability]]
- [[concepts/Actual-use-precision|actual-use precision]]
- [[concepts/Skill-pool-construction|Skill pool construction]]

## 相关实体

- [[entities/Gemini-CLI|Gemini CLI]]
- [[entities/Gemini-3-1-Pro-Preview|Gemini-3.1-Pro-Preview]]
- [[entities/Codex|Codex]]
- [[entities/GPT-5-4|GPT-5-4]]

## 来源提及

- "In Arm 2, explicit agent selection, each task is presented with an available_skills candidate pool and the agent must explicitly choose the skills it would use. The downstream task is not executed."
- "This arm evaluates whether an agent can use task context and skill descriptions to choose helpful skills, without conflating selection with later execution failures."