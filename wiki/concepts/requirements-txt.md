---
type: concept
created: 2026-08-04
updated: 2026-08-04
generation_complete: true
sources:
  - "[[sources/一些常用命令_c2949b]]"
tags:
  - "standard"
aliases:
  - "Python依赖声明文件"
  - "requirements file"
---

# requirements.txt

## 定义
`requirements.txt` 是 Python 生态中一个约定俗成的配置文件，用于声明项目所依赖的外部包及其版本约束。该文件通常命名为 `requirements.txt` 并放置在项目根目录下，通过 `pip` 的 `-r` 选项读取并批量安装依赖。尽管并非 Python 官方强制标准，但它已成为社区事实上的依赖管理标准，是实现环境可复现性的关键一环。

## 关键特征
- **声明式依赖管理**：以纯文本形式列出所需包名与版本，一行一个依赖
- **精确版本冻结**：支持通过 `pip freeze` 生成当前环境的完整包列表及精确版本号，如 `numpy==1.24.2`
- **可复现环境**：其他开发者或部署环境可直接执行 `pip install -r requirements.txt` 还原相同的包集合
- **约定优于配置**：文件名和格式虽非强制性，但被绝大多数 Python 项目、教程和部署平台接纳
- **与 pip 深度集成**：作为 `pip` 工具的原生功能直接支持，无需额外插件

## 应用
- **项目初始化与协作**：新成员克隆仓库后，通过 `pip install -r requirements.txt` 快速同步开发环境
- **部署与持续集成**：在 Dockerfile、CI/CD 流水线中自动安装依赖，保证构建环境一致
- **环境快照**：使用 `pip list --format=freeze > requirements.txt` 生成当前环境的完整快照，便于迁移或重现
- **最小依赖声明**：开发者也可手动编写，仅列出直接依赖，以放宽版本范围（如 `requests>=2.28.0`）
- **文档化依赖**：为项目提供清晰的依赖关系清单，辅助代码审查和安全审计
- **避免路径差异**：相比 `pip freeze`，使用 `pip list --format=freeze` 导出的依赖列表不包含环境特定路径，确保生成的 `requirements.txt` 在不同系统和部署环境中具有更好的一致性和可移植性。
## 相关概念
- [[concepts/环境管理|环境管理]]
- [[concepts/版本控制|版本控制]]

## 相关实体
- [[entities/pip|pip]]

## 来源提及

- "python项目中导出requirements.txt(不含有文件路径)：``pip list --format=freeze > requirements.txt ``" (Python项目中导出requirements.txt(不含有文件路径)：``pip list --format=freeze > requirements.txt``) — [[一些常用命令|一些常用命令]]