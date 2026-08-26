---

type: concept
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [method]
aliases:
  - "Cross-framework robustness"
  - "Framework transfer"
  - "跨框架迁移"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Cross-framework transfer

## 定义

Cross-framework transfer（跨框架迁移）是一种评估程序性知识可移植性的方法：先在某个智能体框架中蒸馏得到技能与工作流记忆，再将其迁移到另一套 prompting 风格、工具接口和执行循环均不同的框架中，用下游任务成功率衡量知识是否真正可迁移，而非比较迁移工件之间的文本相似度。

## 关键特征

- **可移植性被操作化为任务成功率**：以目标框架下的下游任务成功率为衡量标准，而非工件之间的文本相似度
- **框架异构性**：迁移路径跨越不同智能体框架（如 Codex + GPT-5.3-Codex → Gemini CLI + Gemini-3.1-Pro-Preview），目标框架的 prompting 风格、工具接口和执行循环均不同
- **考察对象是程序性知识**：重点验证技能与工作流记忆能否在框架间迁移
- **稳健性差异**：蒸馏为技能的程序性指导比直接迁移工作流记忆更稳健
- **支撑技能的价值主张**：为“技能是标准化、可迁移抽象”的论断提供实证依据

## 应用

- 在 RQ3 中评估 Agent Skills 的可移植性：将 Codex + GPT-5.3-Codex 构建的技能与工作流记忆迁移至 Gemini CLI + Gemini-3.1-Pro-Preview 中验证
- 指导程序性知识的沉淀方式：优先将经验蒸馏为技能而非依赖直接的工作流记忆，以获得更强的跨框架稳健性
- 为跨框架基准测试提供方法论：以任务成功率而非文本相似度作为迁移效果的度量标准

## 相关概念

- [[concepts/outcome-annotation|Outcome annotation]]
- [[concepts/retrieval-bottleneck|Retrieval bottleneck]]
- [[concepts/agent-skills|Agent Skills]]
- [[concepts/workflow-memory|Workflow Memory]]
- [[concepts/procedural-anchoring|Procedural anchoring]]

## 相关实体

- [[entities/Codex|Codex]]
- [[entities/GPT-5-3-Codex|GPT-5-3-Codex]]
- [[entities/Gemini-CLI|Gemini CLI]]
- [[entities/Gemini-3-1-Pro-Preview|Gemini-3-1-Pro-Preview]]

## 来源提及

- "RQ3: Does distilled procedural guidance transfer across agent frameworks? Procedural knowledge may be coupled to the prompting style, tool interface, and execution loop of the framework that produced it."
- "We construct skills and workflow memories from trajectories collected in the primary Codex setting, then evaluate them in Gemini CLI with Gemini-3.1-Pro-Preview."