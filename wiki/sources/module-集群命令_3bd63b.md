---
type: source
created: 2026-08-04
updated: 2026-08-04
source_file: "[[module 集群命令]]"
tags:
  - note
aliases:
  - 集群环境初始化
  - Cluster Init Commands
contentHash: aa-3806fd64
generation_complete: true
---

# 集群命令 - Summary

## 来源
- Original file: [[module 集群命令]]
- Ingested: 2026-08-04

## 核心内容
该文档简要记录了在集群环境中每次启动 cmd 时需要执行的标准初始化流程。首先通过 [[concepts/module-load|module load]] 命令加载 [[entities/anaconda3|anaconda3]] 模块，使 conda 工具链可用；随后执行 `conda.sh` 完成 conda 的 shell 初始化；接着用 `conda activate` 激活预配置环境 [[entities/py310_torch112_cu116|py310_torch112_cu116]]，该环境集成了 Python 3.10、PyTorch 1.12 和 CUDA 11.6；最后通过 `python -V` 确认 Python 版本为 3.10.x。整个过程保证了后续计算任务在统一、可复现的软件栈下运行，是集群使用的基础操作。

## 关键实体
- [[entities/anaconda3|anaconda3]]：Anaconda 发行版的 Python 3 模块，提供 conda 基础。
- [[entities/py310_torch112_cu116|py310_torch112_cu116]]：预配置的 Conda 环境，包含 Python 3.10、PyTorch 1.12 和 CUDA 11.6。

## 关键概念
- [[concepts/module-load|module-load]]：环境模块系统的动态加载方法，用于在集群中加载软件包。

## 要点
- 每次使用 cmd 首先通过 `module load` 加载 anaconda3 模块。
- 执行 `source conda.sh` 完成 conda 的 shell 初始化。
- 激活 `py310_torch112_cu116` 环境，提供 Python 3.10、PyTorch 1.12 和 CUDA 11.6 支持。
- 使用 `python -V` 验证 Python 版本为 3.10.x，确保环境正确加载。