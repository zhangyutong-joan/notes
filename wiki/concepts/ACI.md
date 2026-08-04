---

type: concept
created: 2026-08-04
updated: 2026-08-04
sources: ["[[sources/Points_f210c4]]"]
tags: [term]
aliases:
  - "Agent-Computer Interface"
sources:
  - [[sources/Points_f210c4]]
generation_complete: true
---


# ACI

## 定义
ACI（Agent-Computer Interface，代理计算机接口）是一种专门为 AI Agent 设计的工具接口范式。它强调从 Agent 的认知视角出发，让工具的名称、参数和用法对 Agent 直观、无歧义，从而降低模型误用的概率。与传统面向程序员的 API 设计不同，ACI 将 Agent 视为工具的直接使用者，要求接口本身具备消除错误的设计（防呆），避免强模型因接口表达不清而频繁出错。

## 关键特征
- **Agent 视角设计**：接口的命名、描述和参数都围绕 Agent 的理解能力优化，而非按人类程序员习惯堆砌。
- **防呆设计**：通过强制性约束消除误用可能，例如 SIM 卡的缺角物理限制、微波炉开门断电的安全联锁，理念源自丰田生产体系的「[[concepts/防呆]]」。
- **沟通通道唯一性**：Agent 与工具的交互只能依赖 ACI 本身，若接口设计不良，再强的模型也会反复出错，因为不存在其他信息补偿通道。
- **简洁性与约束性**：借用「[[concepts/保持简单]]」原则，接口越清晰、越少歧义，Agent 的调用成功率越高。

## 应用
- **AI Agent 工具开发**：在设计插件、API、命令行工具供 Agent 调用时，必须遵循 ACI 原则，确保模型能正确解析和执行。
- **自动化工作流设计**：在 [[concepts/Agent]] 进行复杂任务编排时，每个步骤的工具接口都应符合 ACI，减少人工修正成本。
- **模型安全与可靠性**：通过 ACI 的防呆约束，降低 Agent 因误操作而产生的风险，尤其是在涉及文件系统、网络请求或数据修改的场景。

## 相关概念
- [[concepts/防呆]]：源自丰田生产体系的错误预防思想，ACI 将其引入接口设计。
- [[concepts/Agent]]：ACI 的直接使用者和设计服务对象。
- [[concepts/保持简单]]：接口简化是 ACI 的内在要求，避免复杂化引发歧义。

## 相关实体
暂无直接相关实体。

## 来源提及

- "设计好工具接口（ACI，Agent-Computer Interface）。" — [[Points|Points]]
- "ACI 强调的是从 Agent 视角设计接口（让 Agent 容易理解和使用），而非传统 API 从程序员视角设计接口。" — [[Points|Points]]
- "设计不好的工具会让再强的模型也频繁出错——因为模型与工具之间唯一的沟通通道就是接口本身，模糊的接口会被模型放大成系统性的错误。" — [[Points|Points]]