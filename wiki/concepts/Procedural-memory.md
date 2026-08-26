---

type: concept
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [term]
aliases:
  - "程序性记忆"
  - "procedural knowledge"
  - "Procedural Memory"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Procedural memory

## 定义

程序性记忆（Procedural memory）是 LLM 智能体中用于存储和复用先前执行过程知识的一类记忆，涵盖环境设置序列、工具使用模式、调试例程和验证步骤等可操作的程序性经验。在相关论文框架中，程序性记忆被视为一个大的类别，统摄两种具体表示形式：工作流记忆（workflow memory）与技能（skills）。

## 关键特征

- 面向"如何做"：存储的是过程性、可操作的知识，而非陈述性事实
- 内容覆盖执行全流程：环境设置序列、工具使用模式、调试例程、验证步骤
- 作为大类统摄两种具体表示：工作流记忆（workflow memory）保留轨迹级别的执行细节；技能（skills）将程序性知识压缩为标准化制品
- 关键研究问题是表示、检索、调用和抽象各阶段如何影响下游行为
- 对比实验表明，程序性锚定（procedural anchoring）是技能起作用的主要机制，而非显式知识注入

## 应用

- 智能体复用环境配置与工具使用流程，减少重复试错和无效探索
- 借助技能（skills）实现程序性知识在跨任务、跨框架场景中的迁移与复用
- 沉淀调试例程与验证步骤，提升智能体执行任务的稳定性与成功率
- 通过 Terminal-Bench、SkillsBench 等评估基准测量程序性记忆对下游行为的影响

## 相关概念

- [[concepts/workflow-memory|Workflow Memory]]
- [[concepts/agent-skills|Agent Skills]]
- [[concepts/procedural-anchoring|Procedural anchoring]]
- [[concepts/cross-framework-transfer|Cross-framework transfer]]

## 相关实体

- [[entities/Anthropic-Skills|Anthropic-Skills]]
- [[entities/SkillsBench|SkillsBench]]
- [[entities/Terminal-Bench|Terminal-Bench]]
- [[entities/Harbor|Harbor]]

## 来源提及

- "Recent agent systems therefore store and reuse traces of prior execution: environment setup sequences, tool-use patterns, debugging routines, and verification steps that were discovered in earlier runs." (近期的智能体系统因此存储并复用先前执行的轨迹：环境设置序列、工具使用模式、调试例程以及验证步骤，这些都已在早前运行中发现。) — [[raw/Clippings/Demystifying Agent Skills Why They Work—Until They Don’t|Demystifying Agent Skills Why They Work—Until They Don’t]]