---

type: concept
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [term]
aliases:
  - "explicit knowledge injection"
  - "knowledge_injection"
  - "Knowledge Injection"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Knowledge injection

## 定义
Knowledge injection 是论文《Demystifying Agent Skills》中用于标注技能作用机制的标签之一，指注入的工件为智能体提供了其原本缺乏的具体领域知识。在表 2 的机制标注中，它与 procedural_anchor、failure_warning、none、counterproductive 等标签并列。

## 关键特征
- 属于技能作用机制的定性标注标签，用于区分技能发挥作用的不同方式
- 核心判定标准：注入的工件是否补充了智能体原本缺乏的具体领域知识
- 定量结果显示，显式知识注入在技能作用机制中仅占 4.5%
- 与之对照，程序锚定（procedural anchoring）占 65.7%，是技能的主要作用机制
- 该标签帮助研究者区分"提供知识"与"稳定程序"两种不同机制

## 应用
- 在技能效果评估中提供细粒度归因，区分知识补充与程序稳定两种机制
- 用于分析技能价值的核心来源：并非补充缺失事实，而是稳定行动步骤与工具序列
- 为技能设计提供依据：当知识注入占比较低时，提示技能的核心作用在于程序锚定而非事实补充

## 相关概念
- [[concepts/procedural-anchoring|Procedural anchoring]]
- [[concepts/agent-skills|Agent Skills]]
- [[concepts/workflow-memory|Workflow Memory]]
- [[concepts/paired-trajectory-analysis|Paired trajectory analysis]]

## 相关实体
暂无相关实体

## 来源引用
- [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]：表 2 将知识注入列为论文机制标签之一，表明注入的工件提供了智能体原本缺乏的具体领域知识；定量结果显示显式知识注入仅占技能作用机制的 4.5%，而程序锚定占 65.7%。

## 来源提及

- "Procedural anchoring accounts for 65.7% of skill cases, versus 4.5% for explicit knowledge injection, showing that skills stabilize action rather than inject missing facts."
- "The artifact supplies concrete domain knowledge that the agent otherwise lacked."
- "Thus, skills usually do not work by supplying missing facts."