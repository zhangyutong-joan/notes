---

type: concept
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [term]
aliases:
  - "parsed actual-use precision"
  - "execution-time skill-use precision"
  - "实际使用精确率"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# actual-use precision

## 定义

actual-use precision 是论文 RQ4 中用于衡量智能体在执行任务时技能实际使用质量的核心指标。它通过解析智能体的运行轨迹，识别智能体在任务执行过程中实际检查或调用的技能集合，并与基准中人工标注的 ground-truth 技能调用集合进行比较，从而计算出精确率（precision）。

## 关键特征

- 基于运行轨迹解析：该指标不依赖检索阶段的排序结果，而是直接从智能体的实际执行轨迹中提取被检查或调用的技能
- 与 ground-truth 对齐：以人工标注的 ground-truth skill invocation 集合作为参照基准来计算精确率
- 揭示可用性与使用之间的鸿沟：实验显示，当候选技能池从 5 增长到 100 时，actual-use precision 从 29.6% 骤降至 3.3%，而下游成功率仅从 36.4% 略微上升到 39.3%
- 独立于任务成功率：检索准确率不能单独解释任务成功，actual-use precision 的大幅下降表明技能被检索到与实际被使用之间存在显著差距

## 应用

- 用于评估技能检索与技能实际调用之间的一致性，诊断技能池规模扩大后智能体对技能利用效率的退化
- 作为 RQ4 中的核心评测指标，帮助分析 skill pool construction 带来的影响
- 与 [[concepts/retrieval-bottleneck|Retrieval bottleneck]] 相关联，用于揭示检索环节与最终任务执行质量之间并非简单的线性关系

## 相关概念

- [[concepts/retrieval-bottleneck|Retrieval bottleneck]]
- [[concepts/skill-pool-construction|Skill pool construction]]
- [[concepts/ground-truth-skill-invocation|ground-truth skill invocation]]
- [[concepts/semantic-confusability|Semantic confusability]]

## 相关实体

- [[entities/SkillsBench|SkillsBench]]
- [[entities/Codex|Codex]]
- [[entities/Gemini-CLI|Gemini-CLI]]

## 来源提及

- "Averaged across the two reported pairings, downstream success changes only from 36.4% to 39.3% while actual-use precision falls from 29.6% to 3.3%."
- "Gemini’s parsed skill-use precision is low and decreases from 16.9% to 0.7%, while task success remains comparatively flat around 36–39%. Codex starts with higher actual-use precision, 42.3% at pool size 5, but also drops to 5.9% at pool size 100; its task success instead increases from 35.4% to 42.0%."