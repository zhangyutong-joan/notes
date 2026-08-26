---

type: entity
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [product]
aliases:
  - "Codex GPT-5.3-Codex"
  - "GPT-5.3 Codex model"
  - "GPT-5.3 Codex"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# GPT-5.3-Codex

## 描述
GPT-5.3-Codex 是论文在 RQ1–RQ3 中使用的 [[entities/Codex|Codex]] 智能体-模型配对骨干模型。它与 Codex 代理框架组合，在 [[entities/Terminal-Bench|Terminal-Bench 2.0]]、[[entities/Terminal-Bench|Terminal-Bench-Pro]] 和 [[entities/SkillsBench|SkillsBench]] 上评估 Raw、[[concepts/Workflow-Memory|Workflow Memory]] 和 [[concepts/Agent-Skills|Skill]] 三种先验经验表示的效果。论文通过固定该模型配对进行受控实验，得出 Skill 相对 Workflow Memory 的成功率提升，并支持过程锚定等机制性结论。由于 RQ4 执行时该模型在相同评估访问下不再可用，Codex 配对改用 GPT-5.4，因此 RQ4 结果只能进行组内比较，不能直接与 RQ1–RQ3 的数值对照。这一模型版本信息对于理解实验可比性边界至关重要。

## 相关实体
- [[entities/Codex|Codex]]
- [[entities/Gemini-3.1-Pro-Preview|Gemini-3.1-Pro-Preview]]

## 相关概念
- [[concepts/Workflow-Memory|Workflow Memory]]
- [[concepts/Cross-framework-transfer|Cross-framework transfer]]
- [[concepts/Agent-Skills|Agent Skills]]

## 来源提及

- "We instantiate the same experimental protocol with two agent–model pairings: Codex + GPT-5.3-Codex and Gemini CLI + Gemini-3.1-Pro-Preview." (我们以两种智能体-模型配对实例化相同实验协议：Codex + GPT-5.3-Codex 与 Gemini CLI + Gemini-3.1-Pro-Preview。) — [[raw/Clippings/Demystifying Agent Skills Why They Work—Until They Don’t|Demystifying Agent Skills Why They Work—Until They Don’t]]