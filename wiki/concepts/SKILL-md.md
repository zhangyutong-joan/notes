---

type: concept
created: 2026-08-06
updated: 2026-08-06
sources: []
tags: [standard]
aliases:
  - "Agent Skill 入口文件"
  - "Skill 文件"
  - "SKILL.md 文件"
sources:
  - [[sources/Context_Engineering_223615]]
generation_complete: true
---


# SKILL.md

## 定义
SKILL.md 是 Agent Skills 框架中每个技能的入口定义文件，采用 Markdown 格式编写，包含 YAML frontmatter 元数据和详细的流程执行指令。它在渐进式披露机制中承担第二层核心角色：Agent 在推理过程中判断当前任务需要某个技能时，会通过专用的 Skill 工具加载完整的 SKILL.md 内容，其元数据已预先注入上下文，而正文以工具结果的形式出现在对话历史中。

## 关键特征
- **Markdown + YAML frontmatter**：文件本体为普通 Markdown，前置 YAML 块携带技能元数据（如名称、触发条件、依赖工具等）。
- **渐进式披露节点**：作为 [[concepts/渐进式披露|渐进式披露]] 的第二层，元数据在会话启动时即被注入，完整正文仅在需要时才加载，避免一次性塞满上下文。
- **工具结果模式**：正文内容通过 Skill 工具以 `tool result` 机制写入对话，模型无须预加载全部细节。
- **子文档引用**：可通过文件引用（如相对路径）链接至更细粒度的子文档，实现第三层规则的按需加载，形成分层知识结构。
- **标准化入口**：确保每个技能拥有统一的描述格式和加载契约，便于 Agent 理解和调度。

## 应用
- **多技能调度**：在复杂 Agent 系统中，每个技能（如代码审查、数据库查询、文档生成）均有自己的 SKILL.md，Agent 可根据任务动态选择加载。
- **渐进式知识注入**：结合 [[concepts/渐进式披露|渐进式披露]] 策略，用于大型知识库或工具集的分层提示管理，降低 prompt 成本并提升响应质量。
- **可扩展插件体系**：第三方开发者只需按规范提供 SKILL.md 即可扩展 Agent 能力，无需修改核心系统提示。
- **文档与指令一体化**：同时承载技能说明与可执行流程，减少歧义，增强可靠性。

## 相关概念
- [[concepts/Agent-Skills|Agent Skills]]
- [[concepts/渐进式披露|渐进式披露]]
- [[concepts/YAML-frontmatter|YAML frontmatter]]

## 相关实体
（暂无关联实体）

## 来源提及

- "每个 Skill 必须包含一个 `SKILL.md` 文件，元数据就是 `SKILL.md` 开头的 YAML frontmatter（即文件顶部用 `---` 分隔的元数据块），包含 `name` 和 `description` 两个字段。" — [[raw/concept_note/Context_Engineering|Context_Engineering]]
- "当 Agent 判断某个任务需要特定的 Skill 时，通过专用的 Skill 工具**加载完整的 `SKILL.md`**，内容作为 tool result 出现在对话历史中。" — [[raw/concept_note/Context_Engineering|Context_Engineering]]