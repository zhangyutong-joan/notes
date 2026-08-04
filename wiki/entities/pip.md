---
type: entity
created: 2026-08-04
updated: 2026-08-04
generation_complete: true
sources:
  - "[[sources/一些常用命令_c2949b]]"
tags:
  - "product"
aliases:
  - "Python包管理工具"
  - "Pip Installer for Python"
  - "pip"
---

## 描述
pip 是 Python 的标准包管理器，别名 pip包管理工具，用于从 PyPI (Python Package Index) 下载、安装和管理 Python 包及其依赖。在源文件中，演示了 `pip show xxx` 命令查看已安装包的版本、依赖等详细信息，以及 `pip list --format=freeze > requirements.txt` 导出精确版本列表，生成 [[concepts/requirements-txt|requirements.txt]] 文件。通过冻结依赖清单来复现项目运行环境，已成为 Python 项目开发协作、持续集成和生产部署的标准实践。pip 是 Python 开发生态的核心工具，可用于安装如 [[entities/MySQL|MySQL]] 数据库驱动等第三方库，极大地简化了环境配置和依赖管理。

## 相关实体
- [[entities/MySQL|MySQL]]
- [[entities/Python|Python]]
- [[entities/conda|conda]]

## 相关概念
- [[concepts/requirements-txt|requirements.txt]]

## 应用
- 来自 [[sources/一些常用命令_c2949b]]：`pip show xxx` 展示了包信息查看命令，`pip list --format=freeze > requirements.txt` 展示了依赖冻结与导出命令。

## 别名
- pip包管理工具

## 来源提及

- "``pip show xxx``查看包的版本等信息" (``pip show xxx``查看包的版本等信息) — [[一些常用命令|一些常用命令]]
- "``pip list --format=freeze > requirements.txt ``" (``pip list --format=freeze > requirements.txt``) — [[一些常用命令|一些常用命令]]