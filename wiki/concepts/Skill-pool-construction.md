---

type: concept
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [method]
aliases:
  - "candidate-pool construction"
  - "技能池构建"
  - "candidate skill pool"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Skill pool construction

## 定义

Skill pool construction（候选技能池构建）是 RQ4 用于考察技能检索与下游执行的核心实验设计方法。该方法为每个任务构建一个候选技能池，其中包含任务的 ground-truth 技能集与若干干扰项（distractors），通过控制池大小和干扰项类型，系统性地评估 agent 在检索与选择技能时的精确性。池大小在 5、10、20、50、100 之间变化，干扰项按三种方式采样：来自无关技能的 random distractors、嵌入空间近邻的 similar distractors，以及远距离技能的 dissimilar distractors。论文强调 ground-truth 技能集直接来自 [[entities/SkillsBench|SkillsBench]] 的原生任务-技能标注，不从检索输出或 agent 成功中推断。

## 关键特征

- **受控候选池构造**：三个实验——Arm 1 嵌入检索、Arm 2 显式 agent 选择、Arm 3 全池真实执行——共享同一套候选池构造协议，确保跨实验可比性
- **Ground-truth 来源纯净**：技能集直接取自 SkillsBench 的原生任务-技能标注，不依赖检索结果或 agent 行为进行推断
- **多维度干扰项设计**：干扰项分为 random（无关技能）、similar（嵌入空间近邻）和 dissimilar（远距离技能）三类，分别考察不同类型混淆对检索与选择的压力
- **池大小渐进变化**：候选池规模从 5 逐步扩展到 100，用于揭示技能池规模对 precision 的影响趋势
- **与下游执行联动**：候选池不仅用于离线检索评估，还作为 Arm 3 全池真实执行的输入，连接检索质量与端到端任务表现

## 应用

Skill pool construction 主要用于评估 agent 技能系统的检索瓶颈：当候选池中混入语义相近的干扰技能时，嵌入检索和显式 agent 选择都会面临更大的 precision 下降压力。实验结果显示，池越大实际使用的 precision 越低，其中 similar distractors 是离线识别的主要压力源。该方法也适用于对 [[concepts/semantic-confusability|Semantic confusability]] 的定量测量，以及刻画 [[concepts/retrieval-bottleneck|Retrieval bottleneck]] 在不同任务类型下的表现。

## 相关概念

- [[concepts/semantic-confusability|Semantic confusability]]
- [[concepts/retrieval-bottleneck|Retrieval bottleneck]]
- [[concepts/agent-skills|Agent Skills]]
- [[concepts/skill-md|SKILL.md]]

## 相关实体

- [[entities/SkillsBench|SkillsBench]]
- [[entities/Qwen3-Embedding-0-6B|Qwen3-Embedding-0-6B]]
- [[entities/Codex|Codex]]
- [[entities/Gemini-CLI|Gemini-CLI]]

## 来源提及

- "All three experiments use the same controlled candidate-pool construction. Each pool contains the task’s ground-truth skill set and distractors; pool size ranges from 5 to 100, and distractors are sampled as random, semantically similar, or dissimilar skills [^28] [^31] [^22]...." (三个实验使用相同的受控候选池构造。每个池包含任务的 ground-truth 技能集和干扰项；池大小从 5 到 100 不等，干扰项按随机、语义相似或不相似技能采样。) — [[raw/Clippings/Demystifying Agent Skills Why They Work—Until They Don’t|Demystifying Agent Skills Why They Work—Until They Don’t]]