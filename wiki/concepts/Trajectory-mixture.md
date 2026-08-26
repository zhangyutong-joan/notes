---

type: concept
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [method]
aliases:
  - "trajectory composition"
  - "轨迹构成"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Trajectory mixture

## 定义

Trajectory mixture 是论文受控实验中用于组合成功（s，success）与失败（f，failure）源轨迹的实验变量/方法，以 `5s0f`、`3s2f`、`0s5f` 等标签表示成功与失败轨迹的构成比例。该设计在固定轨迹预算下调整成功/失败轨迹的组合方式，系统考察结果标注（Outcome annotation）与失败轨迹比例如何影响 Agent Skills 的构建效用，并隔离经验内容与结果信号的影响。

## 关键特征

- 以 `Ns Mf` 标签记录成功/失败轨迹构成（如 `5s0f` 至 `0s5f`），用于标记不同实验条件
- 每个选定任务先收集足够多的成功与失败轨迹，形成平衡轨迹池（balanced trajectory pool）
- 在固定预算下仅改变成功/失败轨迹构成，不改变轨迹数量
- Workflow Memory 与 Skill 使用同一条源轨迹池，仅表示方式不同
- 隔离“经验内容”与“结果信号”两方面因素的影响
- 是论文 RQ1 与 RQ2 的核心方法设计

## 应用

- 对比不同 mixture 条件下 Agent Skills 构建的效用差异
- 揭示失败轨迹进入轨迹池时标准技能创建通常更强、而无提示变体收益下降的现象
- 以 mixture 标签在论文的大量表格中报告各条件下的成功率

## 相关概念

- [[concepts/Workflow-Memory|Workflow Memory]]
- [[concepts/Agent-Skills|Agent Skills]]
- [[concepts/Outcome-annotation|Outcome annotation]]

## 相关实体

暂无相关实体。

## Mentions in Source

> 论文将 trajectory mixture 描述为对成功（s）与失败（f）源轨迹进行组合的变量，使用 `5s0f` 至 `0s5f` 等标签，并在固定预算下改变成功/失败构成，以隔离经验内容与结果信号的影响。 — [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]

## 来源提及

- "Mixture labels denote the numbers of successful (s) and failed (f) source trajectories." (混合标签表示源轨迹中成功(s)与失败(f)的数量。) — [[raw/Clippings/Demystifying Agent Skills Why They Work—Until They Don’t|Demystifying Agent Skills Why They Work—Until They Don’t]]