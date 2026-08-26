---

type: concept
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [phenomenon]
aliases:
  - "invocation failures"
  - "调用与适用性失败"
  - "SC3"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Invocation and applicability failures

## 定义

Invocation and applicability failures（调用与适用性失败）是技能使用中特有的一种失败类别，在对比性技能使用分类（Contrastive skill-use taxonomy）中编号为 SC3。它指 Agent 在调用技能时未能正确完成"判断技能是否适用、选择性遵循指导、动态调整、适时放弃"的判断链条——机械套用过程性指导、遗漏前提条件、或沿用不再成立的假设，由此产生 `skill_guidance_misapplied_or_ignored` 一类的失败模式。

## 关键特征

- **技能使用特有**：技能并非自动执行，Agent 必须主动判断适用性并决定遵循、调整或放弃，判断失败即构成该类错误
- **核心失败模式**：表现为 `skill_guidance_misapplied_or_ignored`——技能指导被误用或被忽略
- **几乎完全由技能引入**：该模式在 skill-arm 中占 10.0%，而 raw 仅 0.8%、workflow 仅 0.4%
- **SC3 整体显著上升**：从 raw 的 19/528 上升至 skill 的 78/528
- **抽象化的新风险**：可复用的过程性指导在提供便利的同时，也成为误用的潜在来源
- **重新定义技能失败**：将技能失败从"内容本身不好"重构为"调用与适用性判断失败"

## 应用

- 用于技能系统的故障归因：区分"技能内容质量差"与"技能被错误调用或适用性误判"两类不同性质的问题
- 为 Agent 技能设计提供警示：引入可复用技能时，需配套适用性判断与放弃机制，而非默认 Agent 会自然正确使用技能
- 作为对比性 taxonomy 的评估维度之一，用于对比 raw、workflow 与 skill 三种执行模式下的失败分布差异
- 指导评估基准（如 [[entities/SkillsBench|SkillsBench]]）设计失败分类，使抽象化引入的风险可被量化观测

## 相关概念

- [[concepts/agent-skills|Agent Skills]]
- [[concepts/contrastive-skill-use-taxonomy|Contrastive skill-use taxonomy]]
- [[concepts/procedural-anchoring|Procedural anchoring]]

## 相关实体

暂无直接相关实体。

## 来源提及

- "A skill is not self-executing: the agent must decide whether it applies, which parts to follow, how to adapt it, and when to abandon it. This is where many skill-specific failures arise." (技能并非自我执行：Agent 必须判断它是否适用、遵循哪些部分、如何调整以及何时放弃。这正是许多技能特有失败的来源。) — [[raw/Clippings/Demystifying Agent Skills Why They Work—Until They Don’t|Demystifying Agent Skills Why They Work—Until They Don’t]]