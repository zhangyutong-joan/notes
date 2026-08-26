---

type: entity
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [product]
aliases:
  - "Gemini command-line interface"
  - "Gemini command line interface"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Gemini CLI

## 描述

Gemini CLI 是 [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]] 研究中使用的 agent 框架之一，与 [[entities/gemini-3-1-pro-preview|Gemini-3.1-Pro-Preview]] 模型配对运行。它参与 RQ1、RQ2 中围绕 [[concepts/agent-skills|Agent Skills]] 与 [[concepts/workflow-memory|Workflow Memory]] 的对照实验，同时是 RQ3 跨框架迁移实验的目标框架。在检索实验的 Arm 2 与 Arm 3 中，同样采用 Gemini CLI 与该模型配对配置。实验结果显示，Gemini 的解析技能精确率从 16.9% 降至 0.7%，而任务成功率稳定在 36–39% 左右。这一结果与 [[entities/Codex|Codex]] 的实验结论共同说明：精确命中 ground-truth skill 对下游任务成功既非充分也非必要。

## 相关实体

- [[entities/Codex|Codex]]
- [[entities/SkillsBench|SkillsBench]]
- [[entities/Terminal-Bench|Terminal-Bench]]
- [[entities/Qwen3-Embedding-0-6B|Qwen3-Embedding-0-6B]]

## 相关概念

- [[concepts/agent-skills|Agent Skills]]
- [[concepts/workflow-memory|Workflow Memory]]
- [[concepts/procedural-anchoring|Procedural anchoring]]
- [[concepts/skill-use-lifecycle|Skill-Use Lifecycle]]

## 来源提及

- "Gemini’s parsed skill-use precision is low and decreases from 16.9% to 0.7%, while task success remains comparatively flat around 36–39%." (Gemini 解析出的技能使用精确率较低，从 16.9% 降至 0.7%，而任务成功率相对平稳地保持在 36–39% 左右。) — [[raw/Clippings/Demystifying Agent Skills Why They Work—Until They Don’t|Demystifying Agent Skills Why They Work—Until They Don’t]]