---

type: concept
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [method]
aliases:
  - "contrastive trajectory analysis"
  - "paired contrastive trajectory labeling"
  - "配对轨迹分析"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Paired trajectory analysis

## 定义

Paired trajectory analysis 是一种对比式轨迹分析方法，将同一任务在同一设置下由 **Raw**、**Workflow Memory**、**Skill** 三条执行轨迹组成的配对三元组进行比较，以观察技能注入带来的行为变化，并识别注入工件的作用机制。该方法使技能效应可被观察，而不是把技能当作黑箱，支撑了从聚合成功率转向机制归因的分析框架。

## 关键特征

- **配对三元组结构**：对同一任务、同一设置，将 Raw、Workflow Memory、Skill 三条执行轨迹组成配对三元组进行对照
- **大规模归一化**：从异质基准输出中归一化出 8,135 条试验记录
- **抽样开放编码**：对试验记录进行抽样开放编码，构建 528 个配对三元组
- **LLM 评判器分类**：由 LLM 评判器为每个臂分配分类模式，记录成对变化
- **机制归因**：识别注入工件的作用机制，使技能效应可观察而非黑箱
- **人工验证支持**：分类法聚合一致性达 95.8%

## 应用

- 用于 [[entities/SkillsBench|SkillsBench]]、[[entities/Terminal-Bench|Terminal-Bench]] 等基准上的技能效应评估
- 分析 [[concepts/agent-skills|Agent Skills]] 注入前后执行轨迹的行为差异
- 支撑 [[concepts/contrastive-skill-use-taxonomy|Contrastive skill-use taxonomy]] 的分类与机制归因
- 观察 [[concepts/workflow-memory|Workflow Memory]]、[[concepts/procedural-anchoring|Procedural anchoring]] 与 [[concepts/knowledge-injection|Knowledge injection]] 对执行过程的具体影响

## 相关概念

- [[concepts/contrastive-skill-use-taxonomy|Contrastive skill-use taxonomy]]
- [[concepts/agent-skills|Agent Skills]]
- [[concepts/workflow-memory|Workflow Memory]]
- [[concepts/knowledge-injection|Knowledge injection]]
- [[concepts/procedural-anchoring|Procedural anchoring]]

## 相关实体

- [[entities/SkillsBench|SkillsBench]]
- [[entities/Terminal-Bench|Terminal-Bench]]

## 来源提及

- "We design a contrastive study that combines controlled quantitative experiments with paired trajectory analysis."
- "The main unit of analysis is a paired triple. Each triple compares the same task and setting under three arms: raw execution, workflow-memory injection, and skill injection."
- "We construct 528 such triples, covering SkillsBench (144), Terminal-Bench 2.0 (186), and Terminal-Bench-Pro (198)."