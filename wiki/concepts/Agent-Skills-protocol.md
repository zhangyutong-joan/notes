---
type: concept
created: 2026-08-04
updated: 2026-08-06
generation_complete: true
sources:
  - "[[sources/Links_fb9219]]"
  - "[[sources/Context_Engineering_223615]]"
tags:
  - "standard"
aliases:
  - "Agent Skills 协议"
  - "Agent Skills protocol"
  - "Agent Skills"
---

# Agent Skills protocol

## 定义
Agent Skills protocol 是一套旨在标准化 AI 代理（Agent）技能描述、发现与调用的协议。它规范了代理能力的表示方式，使得不同 AI 代理之间可以相互理解并共享技能，从而在多代理系统或协作场景中实现互操作。其官方网站为 agentskills.io，该站点专注于讨论代理技能相关的技术与规范。

## 关键特征
- 标准化技能描述：对代理技能的名称、参数、能力边界进行统一建模
- 技能发现机制：代理可以查询其他代理的技能清单，动态适配任务
- 调用流程规范：定义了技能请求、响应、错误处理等交互流程
- 促进互操作：降低不同框架、不同模型代理之间的集成成本
- SKILL.md 文件以 YAML frontmatter 提供 name 和 description，启动时注入代理对话上下文用于路由决策  
- 代理判断需要调用技能时，通过专用工具
## 应用
- 多代理协作：在分布式任务中，代理根据技能协议自动分配子任务
- 智能助手生态：允许不同开发者开发的 AI 助手共享技能模块
- 企业自动化：标准化技能接口便于集成到工作流引擎中

## 相关概念
*（暂无）*

## 相关实体
*（暂无）*

## 来源提及

- "[Agent Skills](https://agentskills.io/) 协议" ([Agent Skills](https://agentskills.io/) 协议) — [[Links|Links]]