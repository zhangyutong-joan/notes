---

type: concept
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [method]
aliases:
  - "skill-use modes"
  - "12-mode taxonomy"
  - "对比式技能使用分类法"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Contrastive skill-use taxonomy

## 定义

对比式技能使用分类法（contrastive skill-use taxonomy）是一种用于对智能体技能（Agent Skills）的实际效应进行可观察归因的方法学分类体系。它通过对技能执行轨迹进行开放编码，将技能使用结果归纳为有限的一组互斥类别与模式；通过对比不同条件下技能的成功与失败轨迹，区分“技能修复了哪些失败”以及“技能引入了哪些新的失败模式”，从而把对技能效应的评价建立在可观察的行为证据之上。

## 关键特征

- 基于大规模样本：从 8,135 条试验记录中抽样 240 条轨迹进行开放编码
- 编码归纳出 238 个有效标签，合并为三个高级类别和 12 种技能使用模式
- 三个 Skill-use Category 分别为：
  - SC1：成功的程序锚定（successful procedural anchoring）
  - SC2：执行层与验证失败
  - SC3：调用/适用性与边界失败
- 经过独立人工验证，与 LLM 聚合结果的一致性达 95.8%，Cohen’s κ = 0.952
- 采用对比式设计：通过比较成功与失败轨迹来归因技能效应的来源
- 聚焦可观察行为模式，而非不可见的内部推理过程，使归因可重复、可审计

## 应用

- 在 [[entities/SkillsBench|SkillsBench]] 等基准上对技能效应进行结构化分析，评估技能带来的是净收益还是新故障
- 区分 Agent Skills 在 [[entities/Terminal-Bench|Terminal-Bench]] 场景中修复的失败类型与引入的新失败模式
- 为程序锚定（procedural anchoring）的质量提供可度量的观察判据
- 支撑技能使用生命周期（Skill-Use Lifecycle）的追踪，以及工作流记忆（Workflow Memory）相关研究
- 作为“LLM 自动聚合 + 独立人工验证”的标注与分类流程模板，在技能研究中复用

## 相关概念

- [[concepts/agent-skills|Agent Skills]]
- [[concepts/procedural-anchoring|Procedural anchoring]]
- [[concepts/workflow-memory|Workflow Memory]]
- [[concepts/skill-use-lifecycle|Skill-Use Lifecycle]]

## 相关实体

- [[entities/SkillsBench|SkillsBench]]
- [[entities/Terminal-Bench|Terminal-Bench]]

## 来源提及

- "We normalize 8,135 trial records from controlled experiments and retain 238 valid unique labels from 240 open-coded records. We consolidate these observations into a taxonomy of three high-level categories and twelve skill-use modes." (我们规范化对照实验中的 8,135 条试验记录，并从 240 条开放编码记录中保留 238 个有效唯一标签，将这些观察整合为三个高级类别和十二种技能使用模式的分类法。) — [[raw/Clippings/Demystifying Agent Skills Why They Work—Until They Don’t|Demystifying Agent Skills Why They Work—Until They Don’t]]