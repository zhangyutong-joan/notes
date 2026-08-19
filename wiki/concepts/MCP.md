---

type: concept
created: 2026-08-19
updated: 2026-08-19
sources: ["[[sources/Agent的上限可能不在模型而在团队知识_51a636]]"]
tags: [standard]
aliases:
  - "Model Context Protocol"
  - "模型上下文协议"
sources:
  - [[sources/Agent的上限可能不在模型而在团队知识_51a636]]
generation_complete: true
---


# MCP

## 定义

MCP（Model Context Protocol，模型上下文协议）是让 Agent 调用外部工具的标准协议，可类比为 Agent 世界的"USB 接口"——为模型与外部工具之间的交互提供统一、标准化的接入规范。在工具平台选择中，MCP 是目前比较主流的协议；作为工具适配层，它支撑多个 Agent 按需接入，只加载各自需要的工具。

## 关键特征

- 标准工具调用协议：统一 Agent 与外部工具之间的接入方式，类似 USB 接口的标准化作用
- 工具适配层：支撑 N 个 Agent 按需接入，只加载自己需要的工具
- 按业务域拆分 Server：不应把所有工具堆在一个 Server 里，业务之间需要隔离
- 对 token 消耗敏感：工具定义越多，token 消耗越大
- 大模型对单 Server 工具数量有上限，需控制单一 Server 暴露的工具数量

## 应用

- 安全中心团队将底层数据能力按业务域拆分成多个独立的 MCP Server，实现业务隔离与按需加载
- AI 端到端研发平台中，MCP 作为工具适配层，让不同 Agent 只加载自己所需的工具，避免无关工具带来的 token 开销与上下文干扰
- 与渐进式披露、主动注入等机制配合，控制 Agent 每次注入的工具定义规模

## 相关概念

- [[concepts/渐进式披露|渐进式披露]]：按需加载工具定义，避免一次注入全部工具
- [[concepts/主动注入|主动注入]]：平台主动注入知识、工具的方式
- [[concepts/知识包|知识包]]：知识/工具的分发容器，与 MCP Server 按业务域拆分思路相呼应

## 相关实体

- [[entities/ai-端到端研发平台|AI 端到端研发平台]]
- [[entities/安全中心团队|安全中心团队]]

## 来源提及

- "MCP（Model Context Protocol，模型上下文协议）目前是比较主流的协议。"
- "MCP （Model Context Protocol）：让 Agent 调用外部工具的标准协议，类似 Agent 世界的 USB 接口。"
- "关键设计点：不要把所有工具堆在一个 Server 里——大模型对单 Server 工具数有上限，工具太多会增加 token 消耗，业务之间也需要隔离。"