---

type: concept
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [term]
aliases:
  - "skill-use stages"
  - "技能使用管线"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# skill-use pipeline

## 定义
skill-use pipeline（技能使用管线）是将智能体技能效用从端到端成功率中解耦出来的分析框架。它把技能使用过程拆解为多个连续阶段——先前经验如何被表示、技能如何跨智能体框架转移、如何在技能池中被检索、如何被调用，以及在下游执行中如何适配——从而支持在每个阶段分别考察成功与失败机制。论文借此框架组织四个研究问题，分别对应表示方式、成功/失败标注、跨框架转移、技能池检索与下游执行。

## 关键特征
- **阶段化解耦**：不只看聚合的端到端成功率，而是沿技能使用管线逐段归因收益与失败
- **多阶段构成**：涵盖经验表示、跨框架转移、检索、调用、执行时适配等连续环节
- **机制级归因**：使研究者能把结果差异定位到具体机制（如检索瓶颈、调用失败、适用性失败），而非笼统归因于"技能无效"
- **与技能使用生命周期密切相关**：管线视角聚焦单个任务内技能从获取到执行的微观路径，与更宏观的 [[concepts/skill-use-lifecycle|Skill-Use Lifecycle]] 互补
- **支撑控制实验与对比轨迹分析**：是论文开展系统性实验、比较不同智能体轨迹时的核心组织框架

## 应用
- **控制实验设计**：将技能使用分解为独立阶段后，可针对单一变量（如表示方式、标注策略、检索方法）设计对照实验
- **失败诊断**：区分失败的来源——是检索阶段选不出合适技能，还是调用阶段不会正确使用，或是执行阶段适配不当
- **跨框架对比**：用于分析技能在不同智能体框架（如 [[entities/Codex|Codex]] 与 [[entities/Gemini-CLI|Gemini-CLI]]）之间转移时的行为差异
- **基准与评估设计**：为技能基准（如 [[entities/SkillsBench|SkillsBench]]）的度量维度设计提供阶段化视角，避免单一成功率掩盖机制性问题

## 相关概念
- [[concepts/retrieval-bottleneck|Retrieval bottleneck]]
- [[concepts/cross-framework-transfer|Cross-framework transfer]]
- [[concepts/outcome-annotation|Outcome annotation]]
- [[concepts/invocation-and-applicability-failures|Invocation and applicability failures]]
- [[concepts/skill-use-lifecycle|Skill-Use Lifecycle]]

## 相关实体
- [[entities/Codex|Codex]]
- [[entities/Gemini-CLI|Gemini-CLI]]

## 来源提及

- "This perspective suggests that skill utility cannot be understood from end-to-end success alone, but must be analyzed along the stages of the skill-use pipeline."