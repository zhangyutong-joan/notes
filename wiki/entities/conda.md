---
type: entity
created: 2026-08-04
updated: 2026-08-04
generation_complete: true
sources:
  - "[[sources/一些常用命令_c2949b]]"
  - "[[sources/module-集群命令_3bd63b]]"
tags:
  - "product"
aliases:
  - "Anaconda"
  - "Conda"
  - "anaconda3"
---

## 相关概念
- [[concepts/环境管理|环境管理]]
- [[concepts/conda命令|conda命令]]
- [[concepts/Linux命令|Linux命令]]
- [[concepts/远程开发|远程开发]]
- [[concepts/module-load|module load]] (引入集群环境加载模块的关键命令概念，与环境管理紧密相关。)
## 描述
Conda（常被称为 Conda 包管理器）是一个开源的包管理和环境管理系统，最初为 Anaconda Python 发行版设计，但可独立使用。它支持多种编程语言，不仅能管理 Python 包，还能处理二进制依赖和非 Python 库，特别适用于科学计算和机器学习环境。通过 Conda，用户可以创建、激活和切换独立的虚拟环境，从而隔离不同项目的依赖，避免版本冲突。文档中记录了常用 Conda 命令，包括更新 Conda 自身、安装与卸载包、列出环境等，体现了其作为开发工作流核心工具的地位。Conda 与 [[concepts/环境管理|环境管理]] 密切相关，并常与 [[entities/git|git]] 等版本控制工具配合使用，形成完整的项目依赖管理流程。它的快速替代实现 [[entities/mamba|mamba]] 也因其性能优势被越来越多的开发者采用，并且与 conda 相互兼容，共同支持在本地和远程服务器上快速搭建可复现的开发环境。

在集群部署场景中，anaconda3 通常以环境模块的形式提供，用户通过 `module load anaconda3` 命令即可将其激活，使得 conda 命令及由 conda 管理的环境（如预配置的 py310_torch112_cu116）成为可用，从而在不同计算节点间保持一致、可复现的软件栈基础。
## 相关实体
- [[entities/MATLAB|MATLAB]]
- [[entities/mamba|mamba]]
- [[entities/git|git]]
- [[entities/pip|pip]]
- [[entities/py310-torch112-cu116|py310_torch112_cu116]]

## 来源提及

- "conda update -n base conda #update最新版本的conda" — [[一些常用命令|一些常用命令]]
- "conda activate xxxx #开启xxxx环境" — [[一些常用命令|一些常用命令]]
- "conda deactivate  #关闭环境" — [[一些常用命令|一些常用命令]]
- "conda env list #显示所有的虚拟环境" — [[一些常用命令|一些常用命令]]
- "wget https://repo.anaconda.com/archive/Anaconda3-2024.06-1-Linux-x86_64.sh --no-check-certificate # 安装anaconda" — [[一些常用命令|一些常用命令]]
- "conda create --name xxxx python=xxxx #创建新的虚拟环境" — [[一些常用命令_c2949b|一些常用命令_c2949b]]
- "module load anaconda3" — [[module 集群命令|module 集群命令]]