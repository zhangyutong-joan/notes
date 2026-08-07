---

type: concept
created: 2026-08-06
updated: 2026-08-06
sources: ["[[sources/Context_Engineering_223615]]"]
tags: [standard]
aliases:
  - "YAML Frontmatter"
  - "Frontmatter"
  - "YAML 前置元数据"
sources:
  - [[sources/Context_Engineering_223615]]
generation_complete: true
---


# YAML frontmatter

## 定义
YAML frontmatter 是位于 Markdown 文件（典型如 SKILL.md）开头的结构化元数据块，使用三短横线（`---`）作为起始和结束分隔符，通常包含 `name` 和 `description` 两个字段，用于声明技能的基本信息与触发条件。在 Agent Skills 框架中，它构成技能发现的第一层元数据。

## 关键特征
- 位于文件最顶部，由 `---` 包裹的 YAML 键值对组成
- `name` 字段定义技能标识，`description` 字段提供路由规则（使用场景、反例）
- 设计目标是极简常驻 token 开销——只在对话上下文中保留必要的元数据
- 作为渐进式披露机制的第一层，使 Agent 无需加载完整 SKILL.md 即可判断是否激活技能
- 在系统启动时被整体扫描并注入对话上下文，形成全局技能清单

## 应用
- **Agent Skills 系统**：启动时扫描所有已安装技能的 YAML frontmatter，将 `name` 和 `description` 注入系统提示或对话上下文
- **技能路由**：Agent 通过读取 `description` 中声明的使用场景与反例，决定何时触发相应技能
- **轻量元数据管理**：其他 Markdown 工具（如静态站点生成器、笔记应用）也利用 frontmatter 存储标题、标签、日期等元数据

## 相关概念
- [[concepts/渐进式披露|渐进式披露]]
- [[concepts/SKILL.md|SKILL.md]]
- [[concepts/Agent-Skills|Agent Skills]]

## 相关实体
暂无特定关联实体。

## 来源提及

- "元数据就是 `SKILL.md` 开头的 YAML frontmatter（即文件顶部用 `---` 分隔的元数据块），包含 `name` 和 `description` 两个字段。" — [[raw/concept_note/Context_Engineering|Context_Engineering]]
- "`description` 字段是路由决策的关键——它应当足够短（控制常驻的 token 量），但写法要像路由条件而非功能介绍。最直接的写法是 “Use when / Don't use when” 加上几条**反例**（即明确列出“不该触发此 Skill”的场景）。" — [[raw/concept_note/Context_Engineering|Context_Engineering]]