---

type: entity
created: 2026-08-04
updated: 2026-08-04
sources: ["[[sources/一些常用命令_c2949b]]"]
tags: [product]
aliases:
  - "NVIDIA System Management Interface"
  - "NVIDIA GPU监控工具"
sources:
  - [[sources/一些常用命令_c2949b]]
generation_complete: true
---


# nvidia-smi

## 描述
nvidia-smi 是 NVIDIA 官方提供的命令行管理工具（NVIDIA System Management Interface），用于实时监视和管理 [[concepts/GPU|GPU]] 设备。它能够显示 GPU 利用率、显存用量、温度、风扇转速、驱动版本及 CUDA 版本等关键信息。在深度学习训练与 GPU 计算场景中，管理员和开发者常通过 `nvidia-smi` 快速判断 GPU 是否空闲、确认显卡型号（使用 `nvidia-smi -L`）以及检测资源瓶颈。该工具内置于 NVIDIA 驱动中，随驱动一起安装，无需额外配置。

## 相关实体
暂无

## 相关概念
- [[concepts/GPU|GPU]]

## 来源提及

- "nvidia-smi  #查看gpu是否空闲" (nvidia-smi  #查看GPU是否空闲) — [[一些常用命令|一些常用命令]]
- "nvidia-smi -L  #查看gpu型号" (nvidia-smi -L  #查看GPU型号) — [[一些常用命令|一些常用命令]]