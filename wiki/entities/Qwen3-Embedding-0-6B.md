---

type: entity
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [product]
aliases:
  - "Qwen3 embedding model"
  - "0.6B embedding model"
  - "Qwen3 Embedding 0.6B"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Qwen3-Embedding-0.6B

## 描述
Qwen3-Embedding-0.6B 是 Qwen3 Embedding 系列中的一个 0.6B 参数文本嵌入模型。研究中在 RQ4 阶段将其用作离线技能检索工具：将任务指令与技能描述分别编码为向量后，按余弦相似度排序，从 [[entities/skills-bench|SkillsBench]] 中匹配候选技能。该模型还被用来计算语义相似度，以构造随机、相似和不相似的干扰技能。实验显示，嵌入检索的 top-1 精确率从池大小 5 时的 88.3% 降至 100 时的 76.9%，而相似干扰池的下降更为明显。该模型仅作为离线检索诊断工具，其输出并未传入由 [[entities/Codex|Codex]] 或 [[entities/gemini-cli|Gemini CLI]] 驱动的执行实验。

## 相关实体
- [[entities/skills-bench|SkillsBench]]
- [[entities/terminal-bench|Terminal-Bench]]
- [[entities/Codex|Codex]]
- [[entities/gemini-cli|Gemini CLI]]

## 相关概念
- [[concepts/agent-skills|Agent Skills]]
- [[concepts/workflow-memory|Workflow Memory]]
- [[concepts/contrastive-skill-use-taxonomy|Contrastive skill-use taxonomy]]

## 来源提及

- "RQ4 uses Qwen3-Embedding-0.6B [^52] for embedding retrieval, and evaluates explicit selection and downstream execution with Gemini CLI + Gemini-3.1-Pro-Preview and Codex + GPT-5.4." (RQ4 使用 Qwen3-Embedding-0.6B 进行嵌入检索，并用 Gemini CLI + Gemini-3.1-Pro-Preview 和 Codex + GPT-5.4 评估显式选择与下游执行。) — [[raw/Clippings/Demystifying Agent Skills Why They Work—Until They Don’t|Demystifying Agent Skills Why They Work—Until They Don’t]]