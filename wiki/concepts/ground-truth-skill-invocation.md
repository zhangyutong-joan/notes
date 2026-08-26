---

type: concept
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [term]
aliases:
  - "exact ground-truth invocation"
  - "ground-truth skill overlap"
  - "真值技能调用"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# ground-truth skill invocation

## 定义

ground-truth skill invocation 指智能体实际调用或选择的技能集合，与基准为其任务预先标注的规范技能标识（ground-truth skills）完全匹配的现象。它是 [[entities/SkillsBench|SkillsBench]] 在 RQ4 中用于衡量“技能识别与执行是否对齐”的 gold set 标准：如果智能体调用的技能恰好等于任务标注的真值技能集合，则记为一次精确的 ground-truth 调用。

## 关键特征

- 以基准标注作为 gold set：将任务预先标注的规范技能标识作为判断“真值调用”的唯一依据。
- 精确匹配定义：只有实际调用技能集合与标注技能集合完全一致，才构成 ground-truth invocation，部分重叠或范围漂移不计入。
- 既非成功的充分条件，也非严格必要条件：精确调用真值技能不保证任务成功；任务成功也不要求智能体只调用真值技能。
- 多候选检查与范围漂移：智能体经常检查多个候选技能，却无法稳定地把实际使用范围限制在标注真值技能上。
- 非真值技能仍可能提供程序性支持：相关但不在真值集合中的技能，有时依然能为任务执行贡献部分可用的程序性知识。

## 应用

- 作为 RQ4 的评估基准，量化技能识别（identification）与技能执行（execution）之间的对齐程度。
- 用于区分“选对技能”与“真正把技能操作化”之间的差距，推动评估从覆盖匹配转向注意、适配与实际调用。
- 为技能调用失败诊断提供参照：未调用真值技能、只部分调用、或调用后无法有效落地，均可围绕 ground-truth 对齐程度展开分析。

## 相关概念

- [[concepts/actual-use-precision|actual-use precision]]
- [[concepts/retrieval-bottleneck|Retrieval bottleneck]]
- [[concepts/invocation-and-applicability-failures|Invocation and applicability failures]]
- [[concepts/skill-pool-construction|Skill pool construction]]

## 相关实体

- [[entities/SkillsBench|SkillsBench]]
- [[entities/Codex|Codex]]
- [[entities/Gemini-CLI|Gemini-CLI]]

## 来源提及

- "Thus, exact ground-truth skill invocation is neither sufficient nor strictly necessary for success."
- "This combination indicates that execution-time failure is not simply a failure to inspect any skill: agents often inspect or invoke multiple candidates, but do not reliably restrict use to the task’s annotated ground-truth skill."
- "selecting the correct skill does not guarantee task success, while related non-ground-truth skills can still provide useful procedural support."