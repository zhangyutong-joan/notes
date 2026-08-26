---

type: concept
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [method]
aliases:
  - "开放编码"
  - "open-coding pass"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Open Coding

## 定义
Open Coding 是一种归纳式定性编码方法，用于在正式应用固定分类法之前，从原始数据中让初始编码词汇表自然涌现。在本论文中，它被用于构建对比式技能使用分类法的探索性阶段：研究者从受控实验中抽取个体轨迹，通过无头命令行接口将其交给 Claude Sonnet 4.6 进行开放式标注，要求模型输出开放的 `primary_mode_candidate` 字段，而非用预设类别约束编码结果。

## 关键特征
- **归纳式编码**：不依赖预先定义的固定分类法，初始词汇表从数据中自然涌现
- **防止标签污染**：通过无头 CLI 调用模型，并关闭工具使用与会话持久化，避免模型受先前上下文或工具输出影响
- **固定上下文预算截断**：每条轨迹按任务指令 3000 字符、技能制品 3000 字符、轨迹头部 6000 字符、轨迹尾部 12000 字符进行截断
- **聚焦执行末期**：重点关注轨迹尾部，以捕捉执行末期的错误与验证行为
- **开放式输出字段**：模型输出开放的 `primary_mode_candidate` 字段，为后续分类法归纳提供候选标签
- **可追溯的编码结果**：该阶段产生 240 条原始标签记录，其中 238 条被保留为有效唯一标签，并经独立人工校验

## 应用
- 为对比式技能使用分类法（[[concepts/contrastive-skill-use-taxonomy|Contrastive skill-use taxonomy]]）的构建提供初始编码词汇表
- 作为正式分类法应用之前的探索性编码阶段，与配对轨迹分析（[[concepts/paired-trajectory-analysis|Paired trajectory analysis]]）配合使用
- 适用于需要从大规模个体轨迹中归纳行为模式的定性研究场景
- 可用于后续分类法归纳与人工校验流程

## 相关概念
- [[concepts/contrastive-skill-use-taxonomy|Contrastive skill-use taxonomy]]
- [[concepts/paired-trajectory-analysis|Paired trajectory analysis]]

## 相关实体
暂无直接相关实体记录。

## 来源提及

- "Before applying a fixed taxonomy, the pipeline performs an open-coding stage over sampled individual trajectories. The goal is to induce a vocabulary from actual execution failures rather than impose a generic taxonomy from unrelated settings." (在应用固定分类法之前，该流程对抽取的个体轨迹进行开放编码。目标是从实际执行失败中归纳出词汇表，而不是强加一个来自无关情境的通用分类法。) — [[raw/Clippings/Demystifying Agent Skills Why They Work—Until They Don’t|Demystifying Agent Skills Why They Work—Until They Don’t]]