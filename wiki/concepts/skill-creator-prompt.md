---

type: concept
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [method]
aliases:
  - "skill-creator.md"
  - "skill-creator-no-hint.md"
  - "skill generation prompt"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# skill-creator prompt

## 定义

skill-creator prompt 是论文附录中提供的技能生成提示词模板，用于从执行轨迹中蒸馏出可复用的技能文件。它指导模型分析执行轨迹、提取可重复的过程与失败模式，并输出标准化的 [[concepts/skill-md|SKILL.md]] 格式；该提示词在 RQ1 与 RQ2 实验中被用于构建技能，是决定技能蒸馏质量的关键环节。

## 关键特征

- 分两个变体：标准版（skill-creator.md）与 no-hint 版（skill-creator-no-hint.md）
- 标准版允许技能创建者看到成功/失败标注（[[concepts/outcome-annotation|Outcome annotation]]），据此识别失败模式
- no-hint 版刻意移除显式成败标注，要求仅从可观察证据（如命令输出、错误文本、退出状态）推断失败模式
- 指导模型提取可重复过程、步骤、工具命令与失败模式，输出标准化 [[concepts/skill-md|SKILL.md]] 格式
- 明确要求生成通用技能、避免任务特定路径，并使用占位符
- 在 RQ1 与 RQ2 实验中用于从执行轨迹构建技能，是技能蒸馏质量的关键环节

## 应用

- 在 RQ1 和 RQ2 实验中被用于从执行轨迹构建可复用技能
- 作为技能蒸馏的提示词模板，支撑工作流记忆的提取与编码
- 通过标准版与 no-hint 版的对比，评估显式成败标注对技能蒸馏质量的影响
- 用于调研技能在不同目标任务之间的可迁移性与泛化边界

## 相关概念

- [[concepts/skill-md|SKILL.md]]
- [[concepts/outcome-annotation|Outcome annotation]]
- [[concepts/procedural-anchoring|Procedural anchoring]]
- [[concepts/workflow-memory|Workflow Memory]]

## 相关实体

暂无相关实体。

## 来源提及

- "You are a skill generator. Given one or more execution traces from an agent completing a task, you will produce a single reusable skill file that captures the repeatable process."
- "In the no-hint setting, these annotations are removed while preserving the same trajectories and execution protocol."
- "The skill should be general enough to apply to similar tasks, not just the exact task in the traces."