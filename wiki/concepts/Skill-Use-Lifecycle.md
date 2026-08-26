---

type: concept
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [theory]
aliases:
  - "lifecycle view of skill use"
  - "技能使用生命周期"
  - "Skill Lifecycle"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Skill-Use Lifecycle

## 定义

技能使用生命周期（lifecycle view of skill use）是将 agent 技能效用视为沿多个阶段展开的生命周期、而非仅以端到端成功率衡量的核心理论视角。技能效用需要沿**表示（representation）、检索（retrieval）、调用（invocation）、迁移（transfer）与抽象（abstraction）**等阶段逐段分析；技能型自改进的本质不是单纯积累更多记忆，而是构建能够可靠生成、检索和应用程序抽象的 agent。

## 关键特征

- **阶段化分析**：技能效用被拆解为表示、检索、调用、迁移与抽象等阶段，任何单一阶段的失效都会影响端到端表现
- **蒸馏锚点机制**：先验经验被蒸馏为可重用程序锚点（procedural anchors），作为技能在后续任务中被定位和复用的基础
- **上下文兼容性**：当技能在兼容上下文中被检索并调用时有效；上下文不匹配是失效的典型诱因
- **失效模式明确**：当蒸馏指导噪声过多、过度特定、与当前任务不匹配，或被机械执行时，技能失效
- **超越记忆积累**：技能型自改进的核心在于可靠生成、检索与应用程序抽象，而非记忆库的无序扩张

## 应用

- 用于诊断 agent 技能系统失效：不只看失败率，而定位失效发生在生命周期的哪个阶段（检索失败 vs. 调用失败 vs. 迁移失败）
- 指导技能库设计：以"能否被可靠生成、检索、调用"为标准评估技能条目的质量
- 提供评估框架：为 [[entities/SkillsBench|SkillsBench]] 等基准中对技能效用的评测提供理论依据
- 指导程序锚点的蒸馏流程，减少噪声指导与过度特定化

## 相关概念

- [[concepts/Agent-Skills|Agent Skills]]
- [[concepts/Procedural-anchoring|Procedural anchoring]]
- [[concepts/Workflow-Memory|Workflow Memory]]
- [[concepts/Contrastive-skill-use-taxonomy|Contrastive skill-use taxonomy]]

## 相关实体

- [[entities/Codex|Codex]]
- [[entities/Gemini-CLI|Gemini CLI]]
- [[entities/SkillsBench|SkillsBench]]
- [[entities/Terminal-Bench|Terminal-Bench]]

## 来源提及

- "These findings motivate a lifecycle view of skill use. Skills work when prior experience is distilled into reusable procedural anchors that are retrieved and invoked in compatible contexts." (这些发现推动形成技能使用的生命周期观：当先验经验被蒸馏为可重用的程序锚点，并在兼容上下文中被检索和调用时，技能才会发挥作用。) — [[raw/Clippings/Demystifying Agent Skills Why They Work—Until They Don’t|Demystifying Agent Skills Why They Work—Until They Don’t]]