---

type: concept
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [phenomenon]
aliases:
  - "retrieval-utility gap"
  - "skill retrieval bottleneck"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Retrieval bottleneck

## 定义
Retrieval bottleneck 是指技能库规模增大、语义混淆度上升后，检索精度显著下降但下游任务成功率未必同步下降的现象。它揭示出"技能被检索到"与"技能被有效使用"之间的差距：任务失败并不总是因为没找到正确技能，也可能因为找到了但调用不当、不够适配，或执行瓶颈未解决。

## 关键特征
- 检索精度与下游成功率脱钩：技能池从 5 增至 100 时，actual-use precision 从 29.6% 降至 3.3%，但下游成功率基本稳定在 36–39% 附近
- 语义相似的干扰项对离线识别伤害最大
- 精确的 ground-truth 调用既不充分也不必要——命中"正确技能"并非任务成功的充分条件
- 将失败归因从"没找到正确技能"拓宽到"找到了但调用不当、不够适配或执行瓶颈未解决"
- 体现技能可用性（availability）与实际使用效果（actual utility）之间的差距

## 应用
- 指导技能库规模与检索策略的设计，避免仅以离线检索精度作为优化目标
- 在技能评估中区分离线识别精度与实际使用精度，为 [[entities/SkillsBench|SkillsBench]] 等基准提供分析维度
- 用于诊断 Agent 技能系统中"检索命中但任务失败"的案例，引导改进技能调用与执行链路

## 相关概念
- [[concepts/cross-framework-transfer|Cross-framework transfer]]
- [[concepts/agent-skills|Agent Skills]]
- [[concepts/skill-use-lifecycle|Skill-Use Lifecycle]]
- [[concepts/contrastive-skill-use-taxonomy|Contrastive skill-use taxonomy]]

## 相关实体
- [[entities/SkillsBench|SkillsBench]]
- [[entities/Qwen3-Embedding-0-6B|Qwen3-Embedding-0-6B]]
- [[entities/Codex|Codex]]
- [[entities/Gemini-CLI|Gemini-CLI]]

## 来源提及

- "Retrieval is a separate bottleneck: as pools grow from 5 to 100, actual-use precision falls from 29.6% to 3.3%."
- "Confusable distractors impair offline identification, yet downstream success remains stable; exact ground-truth invocation is neither sufficient nor necessary."
- "pool size contributes to the difficulty, but semantic confusability is the more important stressor for identifying the correct procedural artifact."