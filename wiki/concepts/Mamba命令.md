---

type: concept
created: 2026-08-04
updated: 2026-08-04
sources: ["[[sources/一些常用命令_c2949b]]"]
tags: [method]
aliases:
  - "mamba环境管理"
  - "Mamba Commands"
  - "mamba 命令"
sources:
  - [[sources/一些常用命令_c2949b]]
generation_complete: true
---


# Mamba命令

## 定义
Mamba命令是指用于操作Mamba包管理器的命令行指令集合。Mamba本身是一个高性能、跨平台的包管理器，完全兼容conda命令语法，但使用更快的依赖解析器和并行下载机制，能够大幅加速环境创建、包安装等操作。

## 关键特征
- **与conda高度兼容**：绝大部分conda命令可以直接替换为`mamba`，无需改变用户习惯。
- **高性能**：利用C++重写的依赖解析器，速度显著优于conda，尤其在大型环境解析时。
- **跨平台**：支持Linux、macOS和Windows，满足不同开发环境需求。
- **环境管理完备**：提供完整的虚拟环境生命周期管理，包括创建、克隆、激活、删除等。
- **包管理精细**：支持包的安装、卸载、更新、搜索以及缓存清理，常用命令如`mamba install`、`mamba update`、`mamba remove`。
- **缓存控制**：通过`mamba clean --all -y`等命令可有效清理下载和包缓存，释放磁盘空间。

## 应用
- **快速创建项目环境**：例如`mamba create -n py_310 python=3.10`可在秒级内搭建一个纯净的Python 3.10环境。
- **大规模包解析**：在依赖关系复杂的数据科学或机器学习项目中，Mamba能迅速求解兼容版本组合，避免conda解析时漫长的等待。
- **CI/CD加速**：在持续集成流水线中使用Mamba替代conda，显著缩短环境准备时间。
- **日常包维护**：通过`mamba update --all`批量更新所有包，结合`mamba clean`定期清理缓存，保持环境整洁和最新。

## 相关概念
- [[concepts/conda命令|conda命令]]
- [[concepts/Linux命令|Linux命令]]
- [[concepts/环境管理|环境管理]]

## 相关实体
- [[entities/mamba|mamba]]
- [[entities/conda|conda]]

## 来源提及

- "mamba create -n py_310 python=3.10 # 创建新环境: -n 自定义名称 python=版本号" — [[一些常用命令|一些常用命令]]
- "mamba activate py_310 # 激活环境 py_310是刚才新创建的环境名" — [[一些常用命令|一些常用命令]]
- "mamba clean --all -y # 清理所有缓存" — [[一些常用命令|一些常用命令]]