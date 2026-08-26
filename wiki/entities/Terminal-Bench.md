---

type: entity
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [other]
aliases:
  - "Terminal-Bench 2.0"
  - "Terminal-Bench-Pro"
  - "终端基准"
  - "TerminalBench"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Terminal-Bench

## 描述

Terminal-Bench 是一个针对命令行界面（CLI）中困难、真实任务的 agent 基准（benchmark），提供隔离环境和基于测试的验证。本文中的对照实验综合使用 [[entities/skills-bench|SkillsBench]]、Terminal-Bench 2.0 与 Terminal-Bench-Pro：Terminal-Bench 2.0 包含 89 个终端 agent 任务，而 Terminal-Bench-Pro 从 400 个任务的基准中提供 200 个任务的公开划分，覆盖 8 个领域。由于这些任务要求多步执行、调试、服务管理和运行时验证，很多失败是程序性（procedural）错误而非纯事实性错误。这一特性使 Terminal-Bench 适合观察程序性指导——例如 [[concepts/procedural-anchoring|Procedural anchoring]] 与 [[concepts/agent-skills|Agent Skills]]——是否改善执行效果。实验中 Terminal-Bench 通常与 [[entities/Codex|Codex]]、[[entities/gemini-cli|Gemini CLI]] 等 CLI agent 搭配运行。

## 相关实体

- [[entities/skills-bench|SkillsBench]]
- [[entities/Codex|Codex]]
- [[entities/gemini-cli|Gemini CLI]]

## 相关概念

- [[concepts/agent-skills|Agent Skills]]
- [[concepts/procedural-anchoring|Procedural anchoring]]
- [[concepts/workflow-memory|Workflow Memory]]
- [[concepts/skill-use-lifecycle|Skill-Use Lifecycle]]

## 来源提及

- "Terminal-Bench [^19] provides realistic command-line tasks with isolated environments and test-based verification, making it well suited for observing whether procedural guidance improves execution." (Terminal-Bench 提供真实命令行任务、隔离环境和基于测试的验证，因此非常适合观察程序性指导是否改善执行。) — [[raw/Clippings/Demystifying Agent Skills Why They Work—Until They Don’t|Demystifying Agent Skills Why They Work—Until They Don’t]]