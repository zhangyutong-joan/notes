---

type: concept
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [theory]
aliases:
  - "procedural_anchor"
  - "程序锚定"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Procedural anchoring

## 定义

程序锚定（Procedural anchoring，在文中亦称 procedural_anchor）是解释 agent 技能（Skill）有效性的核心机制。它指技能通过提供可用的步骤、顺序、检查清单、工具序列或验证计划，稳定 agent 的动作执行过程。与显式注入事实性知识不同，程序锚定的作用不是补充知识，而是为 agent 的行为提供一个结构化、可复用的执行框架，从而减少执行层面的不稳定和失败。

## 关键特征

- 技能的核心价值在于提供可操作的执行结构（步骤、顺序、检查清单、工具序列、验证计划），而非主要补充事实性知识
- 实证数据支持：procedural_anchor 占技能案例的 65.7%，而显式知识注入仅占 4.5%，说明稳定行动是技能的主要作用
- 显著减少执行层失败，包括环境基础设施、输出格式、服务生命周期和 shell 命令损坏等类别
- 解释了为何将同一经验蒸馏成 Skill 比将其存储为 Workflow Memory 更有优势——Skill 通过程序锚定直接稳定行动

## 应用

- 指导 agent 技能（Skill）的设计：优先将经验编码为可执行程序结构，而非单纯注入知识点
- 在 SkillsBench 与 Terminal-Bench 等基准评估中，用于分析和解释技能提升 agent 执行可靠性的机制
- 为经验蒸馏策略提供理论依据：在技能构建与记忆系统设计之间做出权衡时，程序锚定效应支持优先采用 Skill 形式

## 相关概念

- [[concepts/Agent-Skills|Agent Skills]]
- [[concepts/Workflow-Memory|Workflow Memory]]
- [[concepts/Contrastive-skill-use-taxonomy|Contrastive skill-use taxonomy]]
- [[concepts/Skill-Use-Lifecycle|Skill-Use Lifecycle]]

## 相关实体

- [[entities/SkillsBench|SkillsBench]]
- [[entities/Terminal-Bench|Terminal-Bench]]

## 来源提及

- "Procedural anchoring accounts for 65.7% of skill cases, versus 4.5% for explicit knowledge injection, showing that skills stabilize action rather than inject missing facts." (程序锚定占技能案例的 65.7%，而显式知识注入仅占 4.5%，表明技能稳定的是行动，而不是注入缺失的事实。) — [[raw/Clippings/Demystifying Agent Skills Why They Work—Until They Don’t|Demystifying Agent Skills Why They Work—Until They Don’t]]