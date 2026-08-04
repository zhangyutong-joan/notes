---

type: concept
created: 2026-08-04
updated: 2026-08-04
sources: ["[[sources/Claude-code-命令_e53e82]]"]
tags: [term]
aliases:
  - "CLI commands"
  - "命令行命令"
  - "Claude CLI命令"
sources:
  - [[sources/Claude-code-命令_e53e82]]
generation_complete: true
---


# CLI命令

## 定义
CLI 命令（命令行命令）是在系统 Shell（如 PowerShell 或终端）中直接运行 `claude` 可执行文件时使用的指令，用于启动、继续或管理 Claude Code 交互式会话，与在会话内部使用的[[concepts/斜杠命令|斜杠命令]]不同，CLI 命令在操作系统层面控制工具的行为。

## 关键特征
- 运行环境为系统 Shell，而非 Claude Code 的交互界面
- 命令格式简洁，通常由 `claude` 加上可选的参数或标志构成
- 负责会话生命周期管理：启动、恢复、更新
- 可携带初始提示（prompt）直接进入 REPL，提高启动效率
- 与[[concepts/斜杠命令|斜杠命令]]配合，形成从启动到会话内操作的完整工作流

## 应用
- **启动新会话**：直接执行 `claude` 进入交互式对话
- **继续上次对话**：使用 `claude -c` 恢复前一次未完成的会话
- **更新工具版本**：执行 `claude update` 将 Claude Code 升级到最新版
- **带提示快速开始**：通过 `claude "你的查询"` 在启动同时提交第一个问题，省去进入界面后再提问的步骤

## 相关概念
- [[concepts/斜杠命令|斜杠命令]]

## 相关实体
- [[entities/Claude-Code|Claude-Code]]

## 来源
> 文档中列出了四个常用 CLI 命令：claude 直接进入会话；claude -c 继续上次对话；claude update 更新 Claude Code 版本；claude \“【你的query】\” 带初始提示启动 REPL。 — [[sources/Claude-code-命令_e53e82]]

## 来源提及

- "在powershell里面" (在powershell里面) — [[Claude code 命令|Claude code 命令]]
- "- `claude`：直接进入会话" (- `claude`：直接进入会话) — [[Claude code 命令|Claude code 命令]]
- "- `claude -c` ：继续上次对话" (- `claude -c` ：继续上次对话) — [[Claude code 命令|Claude code 命令]]