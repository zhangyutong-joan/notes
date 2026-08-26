---

type: concept
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [phenomenon]
aliases:
  - "process noise"
  - "过程残留"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Procedural residue

## 定义

Procedural residue（过程残留）是指直接基于工作流记忆（Workflow Memory）构建过程中残留的冗长探索、失败分支和底层调试路径等噪声信息。它不是可复用的程序性知识，而是干扰任务决策的负担。技能（Skills）通过蒸馏与压缩将这些痕迹转化为更干净、可执行的操作程序，从而消除过程残留。

## 关键特征

- 源于工作流记忆对原始执行轨迹的高保真保留，比技能保留了更多附带过程、失败尝试和任务特定细节
- 属于噪声而非可复用知识，会抬高任务决策失败率
- 典型表现为 timeout_budget_exhaustion 在 workflow-memory 条件下达到 10.6%，远高于 raw 的 1.7% 和 skill 的 4.4%
- 解释了技能在同一源轨迹上比工作流记忆提升 +6.06 个百分点的原因：技能消除过程残留，而非仅注入更多经验
- 与 [[concepts/procedural-anchoring|Procedural anchoring]] 形成对照：过程残留是应被去除的负担，procedural anchoring 是应被提炼出的稳定行动结构

## 应用

- 用于解释 Agent 记忆机制的性能差异：工作流记忆比技能更接近原始轨迹，因此更容易受到过程残留的干扰
- 指导技能构建：对工作流轨迹进行蒸馏与压缩，主动剥离失败分支、冗余探索和调试噪声，提炼出干净的操作程序
- 用于区分记忆系统中"应去除的噪声"与"应保留的结构"：过程残留属于前者，[[concepts/procedural-anchoring|Procedural anchoring]] 属于后者

## 相关概念

- [[concepts/workflow-memory|Workflow Memory]]
- [[concepts/procedural-anchoring|Procedural anchoring]]
- [[concepts/agent-skills|Agent Skills]]

## 相关实体

暂无相关实体。

## 来源提及

- "Workflow memory remains closer to the original trajectory and therefore preserves more incidental process, failed attempts, and task-specific details." (工作流记忆更接近原始轨迹，因此保留了更多附带过程、失败尝试和任务特定细节。) — [[raw/Clippings/Demystifying Agent Skills Why They Work—Until They Don’t|Demystifying Agent Skills Why They Work—Until They Don’t]]