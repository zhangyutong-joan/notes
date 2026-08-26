---

type: concept
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [phenomenon]
aliases:
  - "effectiveness-efficiency tradeoff"
  - "效能-效率权衡"
  - "效果-效率权衡"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Effectiveness–efficiency trade-off

## 定义

Effectiveness–efficiency trade-off 描述程序性先验经验的表示形式在**任务成功率（有效性）**与 **token 消耗（效率/成本）**之间的权衡关系。附录 A.9 在 83 个任务的匹配交集上比较发现：Workflow Memory 是最节省 token 的表示，通过清理轨迹噪声大幅降低输入输出 token；Skill 并非在所有情况下都比 Workflow Memory 便宜，但取得最高成功率——较 Raw 提升 5.5 个百分点、比 Workflow Memory 提升 4.8 个百分点，代价是多消耗约 95.3K token。据此，论文将 Skill 解释为**更有效的表示**，将 Workflow Memory 解释为**更省 token 的表示**，说明程序性先验经验需要在性能与上下文成本之间取舍。

## 关键特征

- 权衡的两个维度分别是任务成功率（effectiveness）与 token 成本（efficiency）
- 实证范围来自附录 A.9 中 83 个任务的匹配交集对比
- Skill 取得最高成功率：较 Raw 提升 5.5 个百分点，较 Workflow Memory 提升 4.8 个百分点
- Skill 的代价是额外消耗约 95.3K token，并非在所有情况下都比 Workflow Memory 便宜
- Workflow Memory 通过清理轨迹噪声大幅降低输入输出 token，是最节省 token 的表示
- 体现程序性先验经验的表示形式无法同时最优化有效性与效率，必须做出取舍

## 应用

- 指导 [[concepts/agent-skills|Agent Skills]] 与 [[concepts/workflow-memory|Workflow Memory]] 这类程序性先验经验表示的选型：token 预算受限时优先 Workflow Memory，成功率优先时选择 Skill
- 为 [[concepts/procedural-memory|Procedural memory]] 的性价比评估提供量化依据
- 为 [[entities/SkillsBench|SkillsBench]] 与 [[entities/Terminal-Bench|Terminal-Bench]] 等基准中的表示对比提供分析框架
- 指导程序性先验经验（procedural anchoring）在封装、压缩与检索策略上的取舍设计

## 相关概念

- [[concepts/workflow-memory|Workflow Memory]]
- [[concepts/agent-skills|Agent Skills]]
- [[concepts/procedural-memory|Procedural memory]]
- [[concepts/procedural-anchoring|Procedural anchoring]]

## 相关实体

- [[entities/SkillsBench|SkillsBench]]
- [[entities/Terminal-Bench|Terminal-Bench]]

## 来源提及

- "The result reveals an effectiveness–efficiency trade-off. Workflow Memory is the most token-efficient representation, reducing both input and output tokens relative to Raw trajectories. Skill is not uniformly cheaper than Workflow Memory, but it achieves the highest success rate: it improves over Raw while also reducing token usage, and it trades additional con..." (结果揭示了效能与效率之间的权衡。Workflow Memory 是最节省 token 的表示，相对于 Raw 轨迹同时降低了输入和输出 token。Skill 并非在所有情况下都比 Workflow Memory 便宜，但它取得了最高的成功率：相对于 Raw 提高了成功率，同时减少了 token 使用，并且相对于 Workflow Memory 用额外的上下文换取了更强的执行性能。因此，我们将 Skill 解释为更有效的表示，将 Workflow Memory 解释为更省 token 的表示。) — [[raw/Clippings/Demystifying Agent Skills Why They Work—Until They Don’t|Demystifying Agent Skills Why They Work—Until They Don’t]]