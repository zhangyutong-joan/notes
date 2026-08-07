---

type: concept
created: 2026-08-07
updated: 2026-08-07
sources: ["[[sources/notes_795b78]]"]
tags: [method]
aliases:
  - "Claude上下文分层"
  - "Claude上下文结构"
  - "Claude Agent Context Hierarchy"
sources:
  - [[sources/notes_795b78]]
generation_complete: true
---


# Claude Agent上下文结构

## 定义
Claude Agent 上下文结构是一种分层的上下文组织方案，用于在有限的上下文窗口内高效地管理和向 Claude 代理传递信息。该结构将上下文划分为六个层次，从具体任务描述到长期记忆，每一层承担不同的角色，使代理能够按需获取精准的知识，从而提升执行任务的效果。

## 关键特征
- **六层分层架构**：由 `Your prompt`（任务提示）、`References`（参考材料）、`System prompt`（系统提示）、`CLAUDE.md`（项目约定）、`Skills`（按需技能）和 `Memory`（长期记忆）组成，层级从即时任务到持久记忆逐层深入。
- **上下文窗口高效利用**：通过轻量、按需加载的层次（如 `Skills` 仅在需要时激活）减少上下文膨胀，让代理专注于当前任务相关的信息。
- **明确的角色分离**：
  - `Your prompt` 承载当前具体任务；
  - `References` 提供辅助资料；
  - `System prompt` 定义代理身份和环境；
  - `CLAUDE.md` 记录项目特有的约定和易错点；
  - `Skills` 封装可复用的轻量任务指南；
  - `Memory` 持久化用户的偏好和背景知识。
- **与 Claude 代理深度集成**：此结构专为 Claude 系列模型的代理模式设计，充分利用其指令遵循和长上下文能力，确保各层信息被准确解析和应用。

## 应用
- **复杂任务执行**：在需要多步推理、查阅资料和遵守项目规范的任务中，分层结构帮助代理依次激活对应层次，减少遗漏。
- **项目协作**：团队可在 `CLAUDE.md` 中统一维护项目约定，使所有协作者的 Claude Agent 行为一致。
- **个性化助手**：通过 `Memory` 记住用户偏好，后续交互无需重复说明，提升对话连贯性。
- **工具或技能扩展**：新增的 `Skills` 可作为插件式模块动态加载，适用于代码生成、文档写作、数据分析等垂直场景。

## 相关概念
- [[concepts/Your-prompt|Your prompt]]
- [[concepts/References|References]]
- [[System prompt]]
- [[CLAUDE.md]]
- [[concepts/Skills|Skills]]
- [[concepts/Memory|Memory]]
- [[concepts/上下文工程|上下文工程]]

## 相关实体
- [[entities/Claude-Code|Claude Code]]（Claude Agent 的主要实现）

## 来源提及

- "- **Your prompt：** 告诉 Agent 这次具体要做什么" (你的提示：告诉 Agent 这次具体要做什么) — [[raw/prompt_pool/notes|notes]]
- "- **CLAUDE.md：要轻量，重点写项目坑点；** 告诉 Agent 这个项目有什么特殊约定" (CLAUDE.md：要轻量，重点写项目坑点；告诉 Agent 这个项目有什么特殊约定) — [[raw/prompt_pool/notes|notes]]
- "- **Skills：是轻量指南，需要时加载；** 告诉 Agent 做某类任务时按什么流程" (Skills：是轻量指南，需要时加载；告诉 Agent 做某类任务时按什么流程) — [[raw/prompt_pool/notes|notes]]