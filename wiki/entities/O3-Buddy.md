---

type: entity
created: 2026-08-19
updated: 2026-08-19
sources: ["[[sources/Agent的上限可能不在模型而在团队知识_51a636]]"]
tags: [product]
aliases:
  - "O3-Buddy"
  - "安全中心综合问题问答机器人"
sources:
  - [[sources/Agent的上限可能不在模型而在团队知识_51a636]]
generation_complete: true
---


# O3 Buddy

## 描述

O3 Buddy 是[[entities/安全中心团队|安全中心团队]]的综合问题问答机器人，代表 Agent 作为知识消费者在运营场景中的实际落地。该产品内置复盘 Agent，每周扫描会话记录，遇到回答不了的问题会自动提交 Git MR 补充知识，实现[[concepts/用即积累|用即积累]]。2026 年 6 月运行数据显示，O3 Buddy 月均处理 1097 条对话，采纳率达 92%，月活用户 50 人。在[[concepts/知识飞轮|知识飞轮]]中，O3 Buddy 是「消费—反馈—保鲜」环节的重要实例，用户的每次对话都在为知识库查缺补漏。O3 Buddy 与 OK 机器人合计月均调用 2000 余次，证明知识确实在被 Agent 消费。

## 相关实体

- [[entities/安全中心团队|安全中心团队]]
- [[entities/AI-端到端研发平台|AI 端到端研发平台]]

## 相关概念

- [[concepts/知识飞轮|知识飞轮]]
- [[concepts/用即积累|用即积累]]
- [[concepts/注入即记账|注入即记账]]

## Mentions in Source

> O3 Buddy 与 OK 机器人合计月均调用 2000 余次，证明知识确实在被 Agent 消费。
> ——[[sources/Agent的上限可能不在模型而在团队知识_51a636]]

> 内置复盘 Agent，每周扫描会话记录，遇到回答不了的问题会自动提交 Git MR 补充知识，实现「用即积累」。
> ——[[sources/Agent的上限可能不在模型而在团队知识_51a636]]

## 来源提及

- "例如 安全中心综合问题问答机器人 O3 Buddy 的复盘 Agent 每周扫一遍会话记录，碰到回答不了的问题就自动提 Git MR 补知识。"
- "用户的每次对话实际上都在帮知识库查缺补漏，6 月跑下来月均 1,097 条对话，采纳率 92%。"
- "Agent 调用 | 月均 2,000+ 次（OK 840 + O3 Buddy 1,097），知识真的在被消费"