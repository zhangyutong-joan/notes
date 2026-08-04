---

type: concept
created: 2026-08-04
updated: 2026-08-04
sources: ["[[sources/一些常用命令_c2949b]]"]
tags: [method]
aliases:
  - "Conda虚拟环境管理"
  - "Conda环境命令"
sources:
  - [[sources/一些常用命令_c2949b]]
generation_complete: true
---


# conda命令

## 定义
conda命令是 **[[entities/conda|conda]]** 包管理器提供的命令行工具集合，用于创建、管理、删除虚拟环境，以及安装、更新、卸载软件包。通过 conda 命令，用户可以为不同项目配置独立、可复现的 Python 环境，从而避免依赖冲突并支持多版本共存。它是数据科学、科学计算和软件工程中环境管理的核心方法。

## 关键特征
- **环境全生命周期管理**：提供从创建 (`conda create`)、激活 (`conda activate`)、切换、导出到删除的完整命令链
- **跨平台一致**：在 Windows、macOS、Linux 上使用相同的命令语法
- **与 [[entities/pip|pip]] 互补**：可管理 Python 包和非 Python 系统级依赖，pip 只在 conda 环境内部工作
- **多版本环境隔离**：每个环境拥有独立的解释器和包集合，互不干扰
- **快速创建与复现**：`conda create --name xxxx python=xxxx` 一键生成指定 Python 版本的环境；通过 `environment.yml` 可完整复现环境

## 应用
- **Python 项目隔离**：在同一台机器上维护多个项目，各自使用不同的 Python 版本和依赖包
- **教学与实验**：快速克隆标准环境进行可重复的课堂演示或论文复现
- **自动化工作流**：在 CI/CD 中利用 `conda run` 执行脚本，保证构建环境一致性
- **跨语言工程**：在同一个环境中管理 Python、R、C++ 等不同语言的依赖
- **与 Jupyter 集成**：将 conda 环境注册为 Jupyter kernel，实现笔记本中的环境切换

## 相关概念
- [[concepts/linux-command|Linux命令]]
- [[concepts/mamba-command|Mamba命令]]
- [[concepts/remote-development-techniques|远程开发技巧]]

## 相关实体
- [[entities/conda|conda]]
- [[entities/pip|pip]]
- [[entities/mamba|mamba]]

## 来源引用
> 通过 `conda create --name xxxx python=xxxx` 可以快速创建指定 Python 版本的新环境，`conda activate xxxx` 则用于激活某个环境。

— [[sources/一些常用命令_c2949b]]

## 来源提及

- "conda create --name xxxx python=xxxx #创建新的虚拟环境" — [[一些常用命令|一些常用命令]]
- "conda activate xxxx #开启xxxx环境" — [[一些常用命令|一些常用命令]]
- "conda remove -n xxxx --all  #删除xxxx环境" — [[一些常用命令|一些常用命令]]