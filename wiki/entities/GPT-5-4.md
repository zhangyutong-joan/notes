---

type: entity
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [product]
aliases:
  - "GPT-5.4 model"
  - "Codex GPT-5.4"
  - "GPT 5.4"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# GPT-5.4

## 描述

GPT-5.4 是 OpenAI 的一个大语言模型，在本论文的 RQ4 实验中被用作 [[entities/Codex|Codex]] 的配对模型。由于 [[entities/GPT-5-3-Codex|GPT-5-3-Codex]] 在 RQ4 进行时已无法通过相同的评估访问渠道获得，研究者用 GPT-5.4 作为 Codex 配对的替代模型。该模型被用于显式代理选择（Arm 2）和全候选池真实执行（Arm 3）两项实验，以评估技能检索与任务执行的表现。在 [[entities/SkillsBench|SkillsBench]] 检索实验中，GPT-5.4 配对的 Codex 实际使用精确率从池大小为 5 时的 42.3% 下降到池大小为 100 时的 5.9%，但任务成功率反而上升。论文明确将 RQ4 的结果解释为组内比较，不应与使用 GPT-5.3-Codex 的 RQ1–RQ3 结果直接进行跨模型比较。

## 相关实体

- [[entities/Codex|Codex]]
- [[entities/GPT-5-3-Codex|GPT-5-3-Codex]]
- [[entities/Gemini-CLI|Gemini-CLI]]
- [[entities/Gemini-3-1-Pro-Preview|Gemini-3-1-Pro-Preview]]
- [[entities/SkillsBench|SkillsBench]]

## 相关概念

- [[concepts/embedding-based-retrieval|Embedding-based retrieval]]
- [[concepts/explicit-agent-selection|Explicit agent selection]]
- [[concepts/actual-use-precision|actual-use precision]]
- [[concepts/skill-pool-construction|Skill pool construction]]

## 来源提及

- "GPT-5.3-Codex was no longer available under the same evaluation access when RQ4 was conducted, so GPT-5.4 was used for the Codex pairing in RQ4."
- "We run this selection protocol with Gemini CLI + Gemini-3.1-Pro-Preview and Codex + GPT-5.4."
- "Codex starts with higher actual-use precision, 42.3% at pool size 5, but also drops to 5.9% at pool size 100; its task success instead increases from 35.4% to 42.0%."