---

type: entity
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [product]
aliases:
  - "Harbor evaluation framework"
  - "Harbor framework"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Harbor

## 描述

Harbor 是一个用于在容器环境中评估和优化智能体与模型的评估框架。本研究在下游执行实验中采用 Harbor 的标准评估流程：每任务 5 次唯一试验、并行度 20，并依赖其统一的验证器奖励与指标进行 [[concepts/outcome-annotation|Outcome annotation]]，从而在相同任务上比较 Raw、Workflow Memory 和 Skill 三种条件。Harbor 与 [[entities/SkillsBench|SkillsBench]]、[[entities/Terminal-Bench|Terminal-Bench]] 等基准配套使用，并支撑涉及 [[entities/Codex|Codex]] 与 [[entities/Gemini-CLI|Gemini CLI]] 的评估。它在本研究中承担基准执行与结果采集的基础设施角色，而非被研究的对象；相关分析还涉及 [[concepts/cross-framework-transfer|Cross-framework transfer]] 与 [[concepts/paired-trajectory-analysis|Paired trajectory analysis]]。

## 相关实体

- [[entities/Codex|Codex]]
- [[entities/Gemini-CLI|Gemini CLI]]
- [[entities/SkillsBench|SkillsBench]]
- [[entities/Terminal-Bench|Terminal-Bench]]

## 相关概念

- [[concepts/outcome-annotation|Outcome annotation]]
- [[concepts/cross-framework-transfer|Cross-framework transfer]]
- [[concepts/paired-trajectory-analysis|Paired trajectory analysis]]

## 来源提及

- "Downstream execution experiments follow Harbor’s standard evaluation workflow [^11], with $n=5$ unique trials per task and a parallelism of $20$ unless otherwise noted; retrieval-isolation experiments use one query per task–pool setting."
- "[^11]: Harbor: A framework for evaluating and optimizing agents and models in container environments External Links: [Link](https://github.com/harbor-framework/harbor) Cited by: §A.1, §3.2."