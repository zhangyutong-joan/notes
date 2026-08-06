---

type: concept
created: 2026-08-05
updated: 2026-08-05
sources: ["[[sources/llm-wiki_38393a]]"]
tags: [method]
aliases:
  - "Lint 操作"
  - "Wiki健康检查"
  - "Lint"
sources:
  - [[sources/llm-wiki_38393a]]
generation_complete: true
---


# Lint

## 定义
Lint 是 LLM 辅助 Wiki 知识库中的一种定期健康检查操作。它类似于软件工程中的代码风格检查工具（linter），通过对整个 Wiki 进行系统性审查，发现并报告页面之间的矛盾、过时说法、孤立页面、缺失的交叉引用，以及可以通过网络搜索填补的数据空白。Lint 不仅是纠错手段，还能主动建议需要探索的新问题或需要查找的新资料，帮助维持 Wiki 的一致性、完整性和长期可持续性。

## 关键特征
- **系统性审计**：自动扫描全部页面，而不是针对单个页面触发的操作，类似于全局校对。
- **多维度检查**：涵盖矛盾检测（两个页面说法不一致）、过时信息（来源已更新但 Wiki 未同步）、孤立页面（没有其他页面引用它）、缺失交叉引用（应链接却未链接），以及可填补的数据缺口（如某个实体缺少关键属性，可通过网络检索补充）。
- **主动建议**：除发现现有问题外，还能根据 Wiki 知识结构提出新的探索方向或指出需要引入的外部资料。
- **长期可持续性保障**：作为维护机制，防止 Wiki 随着内容增长而质量下降，将人工维护的负担转交给 LLM 自动处理。
- **非破坏性操作**：Lint 通常只生成报告或建议，不会自动修改页面，需人工或后续流程确认后再执行更改。

## 应用
- **日常维护**：在 Wiki 内容持续积累后，定期运行 Lint 以发现隐蔽的错误，保持知识库可信度。
- **内容整合**：当多个作者或多次 Ingest 操作引入信息时，Lint 可帮助识别同一概念的不同表述或数据冲突。
- **事前预防**：在添加新页面或进行重大编辑前，先执行 Lint 以评估当前 Wiki 健康状况，为修改提供参考。
- **知识发现**：通过分析缺失的交叉引用或数据空白，引导用户补充高价值内容，推动 Wiki 不断完善。

## 相关概念
- [[concepts/Query|Query]]：指向 Wiki 的查询操作，Lint 与 Query 是两种不同的 LLM-Wiki 交互方式，Lint 偏向审查，Query 偏向检索。
- [[concepts/Schema|Schema]]：Wiki 的页面模板和结构规范，Lint 检查时常需以 Schema 为标准判断页面是否缺省必需字段或格式不一致。
- [[concepts/Index-and-Log|Index-and-Log]]：Wiki 的索引和操作日志，Lint 可以基于这些元数据快速定位最近变更或需要复核的区域。
- [[concepts/Raw-Sources|Raw-Sources]]：Lint 检查过时说法时需对比原始资料，确保 Wiki 内容与来源保持一致。

## 相关实体
暂无直接关联的实体页面。Lint 主要与 Wiki 维护流程相关，未来可能关联到具体的 LLM 模型或工具。

## 来源提及

- "Lint. Periodically, ask the LLM to health-check the wiki. Look for: contradictions between pages, stale claims that newer sources have superseded, orphan pages with no inbound links, important concepts mentioned but lacking their own page, missing cross-references, data gaps that could be filled with a web search." (检查。定期让LLM对Wiki进行健康检查。查找：页面之间的矛盾、被新资料取代的过时说法、没有入链的孤立页面、提到但缺乏专属页面的重要概念、缺失的交叉引用、可通过网络搜索填补的数据空白。) — [[raw/Clippings/llm-wiki|llm-wiki]]