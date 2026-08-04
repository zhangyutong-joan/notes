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
  - "Micromamba"
  - "Mamba 包管理器"
---

## 描述
Mamba 是一个高性能的包管理器，旨在作为 [[entities/conda|conda]] 的直接替代品。它使用 C++ 重写了核心依赖解析逻辑，从而大幅加快了包的下载、解析和环境创建速度，尤其在处理复杂或大型环境时优势显著。Mamba 保持了与 Conda 生态的完全兼容，支持相同的 `environment.yml` 文件、通道和包格式，用户可以无缝切换。它提供了与 Conda 几乎一致的命令行接口，涵盖环境创建 (`mamba create`)、激活/退出、删除、克隆，以及包的安装、更新、卸载和缓存清理等常用操作。由于执行效率高，Mamba 已成为数据科学和机器学习开发者进行 [[concepts/环境管理|环境管理]] 时常用的工具之一。在需要快速启动分析环境或与 [[entities/git|git]]、[[entities/MATLAB|MATLAB]] 等工具协同工作的场景中，Mamba 能有效减少等待时间。它还特别适合处理大规模依赖关系的深度学习环境，并提供了一套完整的命令来覆盖日常流程：`mamba info --envs` 可查看所有环境，`mamba create -n <name> python=<version>` 可创建指定 Python 版本的新环境，`mamba install <package>` 用于安装单个或多个包，再配合更新和清理命令即可高效维护环境。

## 相关实体
- [[entities/conda|conda]]
- [[entities/git|git]]
- [[entities/MATLAB|MATLAB]]
- [[entities/python|Python]]

## 相关概念
- [[concepts/环境管理|环境管理]]

## 来源提及

- "mamba create -n py_310 python=3.10" — [[一些常用命令|一些常用命令]]
- "mamba install xxx" — [[一些常用命令|一些常用命令]]
- "mamba remove numpy" — [[一些常用命令|一些常用命令]]
- "mamba clean --all -y" — [[一些常用命令|一些常用命令]]
- "mamba info --envs # 查看mamba下所有环境" — [[一些常用命令_c2949b|一些常用命令_c2949b]]
- "mamba create -n py_310 python=3.10 # 创建新环境: -n 自定义名称 python=版本号" — [[一些常用命令_c2949b|一些常用命令_c2949b]]
- "mamba install xxx # 安装库包，多个包" — [[一些常用命令_c2949b|一些常用命令_c2949b]]