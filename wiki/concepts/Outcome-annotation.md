---

type: concept
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [method]
aliases:
  - "结果标注"
  - "outcome signals"
  - "success/failure annotations"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Outcome annotation

## 定义

Outcome annotation 指在技能构建阶段，将源轨迹的成功/失败标签显式暴露给技能生成器的做法。它通过为每条演示轨迹附加结果信号，使生成器在技能蒸馏过程中能够区分有效经验与失败经验，而非仅依赖轨迹内容本身进行归纳。该概念被用于区分“经验内容本身”与“结果标注”的独立贡献，是理解技能蒸馏为何有效的关键变量。

## 关键特征

- 显式结果信号：以成功/失败标签形式向技能生成器提供轨迹级反馈，区别于轨迹内部的行为序列信息
- 与 no-hint 变体形成对照：消融实验中移除结果标注后即为 no-hint 条件，用于分离“经验内容”与“结果标注”的贡献
- 成功轨迹上的影响有限：仅含成功轨迹时，有无结果标注对技能质量影响不大
- 失败轨迹上作用显著：一旦引入失败轨迹，缺少结果标注会导致技能质量明显下降，表明结果信号在提炼“规避模式”时不可或缺
- 选择与引导功能：结果标注帮助技能蒸馏过程从混合质量的轨迹中筛选有效经验
- 跨模型可复现：该效应在 Codex 与 Gemini CLI 两个配对中均得到重复验证

## 应用

- 技能构建流程设计：在自动技能生成系统中，为源轨迹附加成功/失败标签以提升蒸馏质量
- 失败轨迹利用：从失败演示中提炼“不应做什么”的规避模式，使技能具备更强的鲁棒性
- 消融研究：通过 outcome annotation 与 no-hint 变体的对比（RQ2），量化结果信号对技能效能的贡献
- 多框架技能蒸馏：在 Codex 与 Gemini CLI 等异构 agent 框架间进行技能迁移时，保留结果标注以维持目标环境中的表现

## 相关概念

- [[concepts/agent-skills|Agent Skills]]
- [[concepts/workflow-memory|Workflow Memory]]
- [[concepts/procedural-anchoring|Procedural anchoring]]
- [[concepts/knowledge-injection|Knowledge injection]]
- [[concepts/cross-framework-transfer|Cross-framework transfer]]

## 相关实体

- [[entities/Codex|Codex]]
- [[entities/Gemini-CLI|Gemini-CLI]]

## 来源提及

- "RQ2: What role do outcome signals play in learning from trajectories? Prior trajectories may help because they contain reusable procedures, or because outcome information indicates which behaviors succeeded or failed."
- "In the standard setting, success/failure identities are visible to the skill creator; in the no-hint setting, these annotations are removed while preserving the same trajectories and execution protocol."