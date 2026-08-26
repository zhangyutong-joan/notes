---

type: entity
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [product]
aliases:
  - "Gemini 3.1 Pro Preview"
  - "Gemini-3.1-Pro model"
  - "Gemini 3.1 Pro"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Gemini-3.1-Pro-Preview

## 描述

Gemini-3.1-Pro-Preview 是论文中 [[entities/Gemini-CLI|Gemini-CLI]] 智能体配对所使用的骨干模型，贯穿 RQ1–RQ4 的实验设计。它与 Gemini CLI 组合，在 [[entities/Terminal-Bench|Terminal-Bench]]、[[entities/SkillsBench|SkillsBench]] 和 Terminal-Bench-Pro 上评估技能注入、工作流记忆以及 outcome annotation 消融的效果。

在 RQ4 的检索与真实执行实验中，该模型的解析技能使用精确率随技能池增大从 16.9% 降至 0.7%，而下游任务成功率保持在 36–39% 左右，说明 [[concepts/Retrieval-bottleneck|Retrieval bottleneck]] 与任务成功并非一一对应。该模型还用于跨框架迁移实验，承接从 [[entities/Codex|Codex]] 轨迹中构建的技能与工作流记忆，验证 [[concepts/Cross-framework-transfer|Cross-framework transfer]] 的可行性。

## 相关实体

- [[entities/Gemini-CLI|Gemini-CLI]]
- [[entities/Codex|Codex]]
- [[entities/GPT-5.3-Codex|GPT-5.3-Codex]]
- [[entities/Terminal-Bench|Terminal-Bench]]
- [[entities/SkillsBench|SkillsBench]]

## 相关概念

- [[concepts/Retrieval-bottleneck|Retrieval bottleneck]]
- [[concepts/actual-use-precision|actual-use precision]]
- [[concepts/Cross-framework-transfer|Cross-framework transfer]]
- [[concepts/Skill-pool-construction|Skill pool construction]]

## 来源提及

- "For RQ1–RQ2, the skill-vs-procedural-memory and no-hint protocols are implemented for two agent–model pairings: Codex + GPT-5.3-Codex and Gemini CLI + Gemini-3.1-Pro-Preview." (在 RQ1–RQ2 中，技能-vs-程序性记忆与无提示协议以两种智能体-模型配对实现：Codex + GPT-5.3-Codex 与 Gemini CLI + Gemini-3.1-Pro-Preview。) — [[raw/Clippings/Demystifying Agent Skills Why They Work—Until They Don’t|Demystifying Agent Skills Why They Work—Until They Don’t]]