---
type: source
created: 2026-08-07
updated: 2026-08-07
source_file: "[[raw/prompt_pool/notes.md]]"
tags: [other]
aliases: ["Prompt工程笔记", "提示词积累与对话管理笔记"]
contentHash: 57b-eec874a7
generation_complete: true
---

# 提示词积累笔记 - Summary

## 来源
- Original file: [[raw/prompt_pool/notes.md]]
- Ingested: 2026-08-07

## 核心内容
本笔记汇集了提示词优化项目和对话管理实践。第一部分列举了自动化提示词工程资源，包括[[entities/Enhance_your_prompts_with_meta_prompting|元提示优化示例]]、[[entities/AutoPrompt-Studio|AutoPrompt Studio]]、[[entities/PromptBreeder|PromptBreeder]]、[[entities/promptomatix|promptomatix]]以及[[entities/aishort提示词库|aishort提示词库]]。第二部分提出对话长度控制原则，强调单次对话应保持在2～3万字，并在质量下降时切换到新对话，切换前提取摘要，最终手动备份记录。第三部分详细描述了Claude Agent的六层上下文结构（[[concepts/Your-prompt|Your prompt]]、[[concepts/References|References]]、System prompt、CLAUDE.md、Skills、[[concepts/Memory|Memory]]），要求CLAUDE.md轻量且聚焦项目陷阱，Skills按需加载。

## 关键实体
- [[entities/Enhance_your_prompts_with_meta_prompting|Enhance_your_prompts_with_meta_prompting]]
- [[entities/AutoPrompt-Studio|AutoPrompt-Studio]]
- [[entities/PromptBreeder|PromptBreeder]]
- [[entities/promptomatix|promptomatix]]
- [[entities/aishort提示词库|aishort提示词库]]

## 关键概念
- [[concepts/Meta-prompting|Meta-prompting]]
- [[concepts/Intent-based-Prompt-Calibration|Intent-based-Prompt-Calibration]]
- [[concepts/对话长度控制|对话长度控制]]
- [[concepts/摘要提取|摘要提取]]
- [[concepts/手动备份对话记录|手动备份对话记录]]
- [[concepts/Claude-Agent上下文结构|Claude-Agent上下文结构]]
- [[concepts/Your-prompt|Your-prompt]]
- [[concepts/References|References]]
- [[concepts/Memory|Memory]]

## 要点
- 元提示、意图校准和进化算法可自动化提示优化，参考项目如[[entities/AutoPrompt-Studio|AutoPrompt Studio]]和[[entities/PromptBreeder|PromptBreeder]]
- 对话长度应控制在2～3万字，质量下降即换会话，换前提取摘要并手动备份
- Claude Agent通过Your prompt、References、System prompt、CLAUDE.md、Skills、Memory六层结构按需加载上下文，CLAUDE.md轻量记录项目坑点，Skills作为轻量任务指南