---

type: entity
created: 2026-08-04
updated: 2026-08-04
sources: ["[[sources/一些常用命令_c2949b]]"]
tags: [other]
aliases:
  - "GPU"
  - "图形处理单元"
  - "Graphics Processing Unit"
sources:
  - [[sources/一些常用命令_c2949b]]
generation_complete: true
---


# NVIDIA GPU

## 描述
NVIDIA GPU（图形处理单元）是深度学习训练与推理的核心硬件加速器，通过高并行计算能力显著提升模型运算效率。在远程服务器环境中，常使用 [[entities/nvidia-smi|nvidia-smi]] 或 `gpustat -i` 命令实时查看 GPU 使用状态、温度与显存占用。结合 [[entities/Python|Python]] 深度学习框架（如 PyTorch），可通过 `torch.cuda.is_available()` 与 `torch.cuda.device_count()` 确认 CUDA 可用性及可用设备数量。这些工具与接口让开发者能够在 [[entities/Jupyter-Notebook|Jupyter-Notebook]] 等交互式环境中合理分配 GPU 资源，保障分布式训练与远程实验的稳定性。

## 相关实体
- [[entities/Python|Python]]
- [[entities/Jupyter-Notebook|Jupyter-Notebook]]
- [[entities/nvidia-smi|nvidia-smi]]
- [[entities/conda|conda]]
- [[entities/mamba|mamba]]

## 相关概念
- [[concepts/远程开发|远程开发]]
- [[concepts/远程开发技巧|远程开发技巧]]
- [[concepts/环境管理|环境管理]]
- [[concepts/Linux命令|Linux命令]]

## 来源引用
- “使用 `nvidia-smi` 查看 GPU 使用状态和型号，`gpustat -i` 实时监视 GPU 占用情况。” — [[sources/一些常用命令_c2949b]]
- “通过 PyTorch 的 `torch.cuda.is_available()` 和 `torch.cuda.device_count()` 确认 CUDA 可用性和设备数量。” — [[sources/一些常用命令_c2949b]]

## 来源提及

- "nvidia-smi  #查看gpu是否空闲" — [[一些常用命令_c2949b|一些常用命令_c2949b]]
- "nvidia-smi -L  #查看gpu型号" — [[一些常用命令_c2949b|一些常用命令_c2949b]]
- "gpustat -i # 实时监视GPU使用情况(删去-i就不实时)" — [[一些常用命令_c2949b|一些常用命令_c2949b]]
- "torch.cuda.is_available()  #查看gpu是否可用" — [[一些常用命令_c2949b|一些常用命令_c2949b]]