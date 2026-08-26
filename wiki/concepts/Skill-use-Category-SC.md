---

type: concept
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don't_b13e06]]"]
tags: [term]
aliases:
  - "SC"
  - "技能使用类别"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Skill-use Category (SC)

## 定义

Skill-use Category（SC）是对比式技能使用分类法中的顶层分类标签，将 12 个细粒度成功/失败模式归纳为三个高层类别：**SC1（成功的过程锚定）**、**SC2（执行层与验证失败）**、**SC3（调用、适用性与边界失败）**。该标签用于分解"技能何时有帮助、为何有效、在何处失败"这一核心研究问题。

## 关键特征

- **三分类顶层结构**：SC1 代表成功的过程锚定，涵盖智能体自主成功或先验经验提供有效指导的情形；SC2 涵盖环境搭建、输出格式、服务生命周期、shell 执行、算法实现和运行时验证等执行层与验证失败；SC3 涵盖指导被误用、过度应用、忽略或受外部限制等调用与适用性失败
- **归纳 12 个细粒度模式**：将技能使用的具体成功/失败模式聚合为三个可比较的高层类别
- **支持对比分析**：实验数据显示，技能臂比工作流记忆臂将更多轨迹移入 SC1，同时减少 SC2 类失败、增加 SC3 类失败
- **定位为顶层标签**：作为对比式技能使用分类法（Contrastive skill-use taxonomy）的一级分类入口，向下可细分至具体失败类型

## 应用

- **失败归因分析**：用于对技能型智能体的运行轨迹进行分类，判断技能在何种环节失效或生效
- **机制对比评估**：支持比较不同记忆与技能机制（如技能臂 vs 工作流记忆臂）在成功锚定与失败类型上的分布差异
- **技能系统改进**：通过 SC2 与 SC3 的细分失败统计，为技能库的修复、文档完善与调用策略调整提供依据

## 相关概念

- [[concepts/contrastive-skill-use-taxonomy|Contrastive skill-use taxonomy]]
- [[concepts/execution-layer-failures-sc2|Execution-layer failures (SC2)]]
- [[concepts/invocation-and-applicability-failures|Invocation and applicability failures]]
- [[concepts/procedural-anchoring|Procedural anchoring]]

## 相关实体

- [[entities/Anthropic-Skills|Anthropic-Skills]]
- [[entities/SkillsBench|SkillsBench]]
- [[entities/Harbor|Harbor]]
- [[entities/Terminal-Bench|Terminal-Bench]]

## 来源提及

- "Each trajectory is assigned a Skill-use Category (SC), which serves as its top-level taxonomy label. The three SCs group the 12 fine-grained modes summarized in Table 11." (每条轨迹都被分配一个 Skill-use Category（SC）作为其顶层分类标签。三个 SC 将表 11 中总结的 12 个细粒度模式进行分组。) — [[raw/Clippings/Demystifying Agent Skills Why They Work—Until They Don’t|Demystifying Agent Skills Why They Work—Until They Don’t]]