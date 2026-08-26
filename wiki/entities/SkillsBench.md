---

type: entity
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [other]
aliases:
  - "SkillsBench benchmark"
  - "技能基准"
  - "SkillsBench 基准"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# SkillsBench

## 描述

SkillsBench 是一个用于衡量结构化技能在多样任务上表现的基准，由 86 个任务、覆盖 11 个领域组成，专为基于技能的程序性复用设计。该基准提供原生的任务-技能标注，可用于计算技能检索的精确率与召回率，因此在 RQ4 中被用作核心评估工具。研究利用 SkillsBench 构建受控候选技能池，考察池大小与干扰项类型对技能识别和执行的影响。实验结果显示，当候选技能池规模从 5 增大到 100 时，实际使用的精确率从 29.6% 下降至 3.3%，但下游任务成功率保持相对平稳。这一发现帮助作者区分了"找到正确技能"与"任务成功"并非一一对应的关系。SkillsBench 与 [[entities/terminal-bench|Terminal-Bench]] 共同构成本研究的评估套件，为验证 [[concepts/agent-skills|Agent Skills]] 的 [[concepts/procedural-anchoring|Procedural anchoring]] 机制提供了量化依据。

## 相关实体

- [[entities/terminal-bench|Terminal-Bench]]
- [[entities/qwen3-embedding-0.6b|Qwen3-Embedding-0.6B]]
- [[entities/Codex|Codex]]
- [[entities/gemini-cli|Gemini CLI]]

## 相关概念

- [[concepts/agent-skills|Agent Skills]]
- [[concepts/procedural-anchoring|Procedural anchoring]]
- [[concepts/workflow-memory|Workflow Memory]]
- [[concepts/contrastive-skill-use-taxonomy|Contrastive skill-use taxonomy]]

## 来源提及

- "SkillsBench [^17] measures structured skills across diverse tasks, while SWE-Skills-Bench [^10] studies the marginal utility of skill documents in real-world software-engineering settings." (SkillsBench 衡量结构化技能在多样任务上的表现，而 SWE-Skills-Bench 研究技能文档在真实软件工程环境中的边际效用。) — [[raw/Clippings/Demystifying Agent Skills Why They Work—Until They Don’t|Demystifying Agent Skills Why They Work—Until They Don’t]]