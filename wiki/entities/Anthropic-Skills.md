---

type: entity
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [project]
aliases:
  - "Anthropic skills repository"
  - "Skills: Public Repository for Agent Skills"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Anthropic Skills

## 描述

Anthropic Skills 是 Anthropic 公开的 Agent Skills 仓库，论文将其作为 [[concepts/agent-skills|Agent Skills]] 概念的代表性来源引用。该仓库定义了将可复用程序性知识封装为技能工件的方式，例如通过 [[concepts/skill-md|SKILL.md]] 文件描述技能的能力与使用协议。论文多处引用其 GitHub 仓库链接，将其作为技能格式与使用方式的权威背景。

研究中，技能被放置在执行环境中作为可复用程序资源使用，而不是完全内联进初始上下文，这一用法遵循 Anthropic Skills 所代表的协议。该仓库的出现是论文研究背景中"skills 成为一种引人注目的抽象"这一判断的现实基础。虽然本文并非围绕该仓库本身展开，但它为理解技能的封装格式与实际使用方式提供了关键背景，也是讨论 [[entities/Codex|Codex]]、[[entities/Gemini-CLI|Gemini-CLI]] 等系统中技能资源时的基础参照之一。

## 相关实体

- [[entities/Codex|Codex]]
- [[entities/Gemini-CLI|Gemini-CLI]]

## 相关概念

- [[concepts/agent-skills|Agent Skills]]
- [[concepts/skill-md|SKILL.md]]

## 来源提及

- "[^2]: Anthropic Skills: Public Repository for Agent Skills. Note: Accessed: 2026-05-23 External Links: [Link](https://github.com/anthropics/skills) Cited by: §A.1, §1, §3.2."
- "In skill-based conditions, skills are placed in the execution environment as reusable procedural resources rather than fully incorporated into the initial context [^2]."