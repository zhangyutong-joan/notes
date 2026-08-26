---

type: concept
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [method]
aliases:
  - "工作流记忆"
  - "workflow memories"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Workflow Memory

## 定义

Workflow Memory（工作流记忆）是一种记忆表示方法：它将智能体过去执行任务时产生的轨迹（trajectories）总结为行动级程序（action-level procedures），供未来任务直接重用。与 Skill 不同，Workflow Memory 不进行标准化压缩，而是保留经过清理的程序性流程，作为可回放的操作序列存储。

## 关键特征

- **行动级程序表示**：将历史轨迹提炼为可执行的步骤序列，而非抽象的策略描述
- **与 Skill 同源构建**：两者从相同的轨迹池（trajectory pool）中构建，但处理方式不同——Workflow Memory 保留清理后的程序性流程，Skill 则压缩为标准化 SKILL.md
- **携带过程噪声**：保留有用程序证据的同时，也携带无关探索、失败分支和冗长过程，导致超时（timeout）与漂移（drift）增加
- **成功率低于 Skill**：实验表明 Skill 相对 Workflow Memory 平均提升 6.06 个百分点
- **Token 成本最优**：在各类记忆表示中，Workflow Memory 是最节省 token 的表示方式，但效果不如 Skill

## 应用

Workflow Memory 在智能体技能研究中作为对照条件（baseline condition）使用，用于衡量标准化技能表示（如 SKILL.md）相对于原始程序性记忆的增益。其典型应用场景包括：

- **轨迹重用实验**：评估从历史执行轨迹中提取程序性知识是否足以支撑未来任务的完成
- **技能压缩对照**：作为 Skill 的上游表示，揭示"清理轨迹"与"标准化压缩"之间的性能差距
- **Token 受限环境**：在 token 预算极为紧张的场景下，Workflow Memory 因其最节省 token 的特性而具备一定吸引力，但需权衡成功率损失

## 相关概念

- [[concepts/agent-skills|Agent Skills]]
- [[concepts/procedural-anchoring|Procedural anchoring]]
- [[concepts/skill-use-lifecycle|Skill-Use Lifecycle]]

## 相关实体

- [[entities/SkillsBench|SkillsBench]]
- [[entities/Terminal-Bench|Terminal-Bench]]
- [[entities/Codex|Codex]]
- [[entities/Gemini-CLI|Gemini-CLI]]

## 来源提及

- "Workflow memories summarize past trajectories into action-level procedures for future tasks." (工作流记忆将过去轨迹总结为行动级程序，以供未来任务使用。) — [[raw/Clippings/Demystifying Agent Skills Why They Work—Until They Don’t|Demystifying Agent Skills Why They Work—Until They Don’t]]