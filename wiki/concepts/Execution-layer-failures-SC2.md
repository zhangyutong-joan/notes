---

type: concept
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [term]
aliases:
  - "SC2 execution-layer and verification failures"
  - "执行层失败"
  - "SC2"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Execution-layer failures (SC2)

## 定义
Execution-layer failures (SC2) 是 Demystifying Agent Skills 论文提出的对比式技能使用分类法中的第二类顶层失败类别，指 agent 在执行阶段因环境配置、输出格式、服务生命周期、shell 命令、算法实现和运行时验证等方面的缺陷而导致的任务失败，属于执行层及验证性失败。

## 关键特征
- 是对比式技能使用分类法的顶层类别之一（编号 SC2），与 [[concepts/Invocation-and-applicability-failures|Invocation and applicability failures]] 并列
- 涵盖六个具体失败模式：`environment_infrastructure_failure`、`output_format_schema_mismatch`、`background_service_lifecycle_failure`、`shell_code_corruption`、`algorithmic_logic_error`、`static_verification_without_runtime`
- 技能注入显著降低 SC2 类失败发生率：raw 组 37.3%、workflow memory 组 33.3% → skill 组 23.5%
- `environment_infrastructure_failure` 改善最明显：raw 执行的 5.3% → skill 的 0.2%
- `algorithmic_logic_error` 和 `static_verification_without_runtime` 在技能注入后仍持续存在，属于技能难以完全消除的深层问题

## 应用
- 用于在 [[entities/SkillsBench|SkillsBench]] 和 [[entities/Terminal-Bench|Terminal-Bench]] 等评测中对 agent 失败进行细粒度分类，量化执行层失败的构成与占比
- 用于评估技能注入对执行稳健性的实际提升效果，特别是环境基础设施类失败的大幅下降
- 指导技能设计：技能能提高执行稳健性，但不能替代深层问题重构或更强的运行时验证，提示评测者关注技能覆盖面之外的残余失败模式

## 相关概念
- [[concepts/Agent-Skills|Agent Skills]]
- [[concepts/Workflow-Memory|Workflow Memory]]
- [[concepts/Invocation-and-applicability-failures|Invocation and applicability failures]]
- [[concepts/Contrastive-skill-use-taxonomy|Contrastive skill-use taxonomy]]

## 相关实体
- [[entities/SkillsBench|SkillsBench]]
- [[entities/Terminal-Bench|Terminal-Bench]]

## 来源提及

- "SC2 captures execution-layer and verification failures, including environment setup, output formatting, service management, shell execution, algorithmic implementation, and runtime validation." (SC2 捕获执行层和验证性失败，包括环境设置、输出格式、服务管理、shell 执行、算法实现和运行时验证。) — [[raw/Clippings/Demystifying Agent Skills Why They Work—Until They Don’t|Demystifying Agent Skills Why They Work—Until They Don’t]]