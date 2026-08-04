---
type: concept
created: 2026-08-04
updated: 2026-08-04
generation_complete: true
sources:
  - "[[sources/一些常用命令_c2949b]]"
tags:
  - "method"
aliases:
  - "Linux常用命令"
  - "Linux系统命令"
  - "Linux系统管理"
---

## 相关概念
- [[concepts/conda命令|conda命令]]
- [[concepts/远程开发技巧|远程开发技巧]]
- [[concepts/Mamba命令|Mamba命令]]
- [[concepts/vim命令模式|vim命令模式]]

## 相关实体
- [[entities/Vim|Vim]]
- [[entities/nvm|nvm]]
- [[entities/npm|npm]]
- [[entities/Node-js|Node-js]]

## 定义
Linux命令是Linux操作系统中用于完成系统管理、文件操作、进程控制与硬件资源监控的文本指令集合。在本笔记中聚焦于一组面向开发运维的实用命令，覆盖用户创建（`useradd`）、密码设置（`passwd`）、系统服务重启（`systemctl`）、磁盘空间分析（`du`、`df`）、文件属主修改（`chown`）以及GPU状态实时监控（`gpustat`）等场景，帮助使用者在本地或远程Linux环境中快速完成运维任务。

## 关键特征
- **覆盖面广**：涉及用户管理、磁盘分析、权限修改、系统重启与GPU监控等多个运维维度。
- **组合性强**：多个命令可通过管道、重定向或Shell脚本组合，实现自动化运维流程。
- **即时反馈**：直接输出文本结果，便于快速判断系统状态（如`df -h`展示文件系统使用率，`du -h -x --max-depth=1`显示当前目录下各子文件夹的空间占用）。
- **实时监控能力**：通过`gpustat -i`等命令提供GPU利用率的动态刷新视图，适用于深度学习等计算密集型场景。
- **轻量无图形依赖**：纯命令行操作，适合远程SSH终端或脚本化环境。

## 应用
- **用户与权限审计**：在多人共享服务器上，使用`useradd`、`passwd`创建账户并设置密码，用`chown`、`chmod`调整文件属主与访问权限。
- **空间清理**：运行`du -h -x --max-depth=1`快速定位当前目录各子文件夹的磁盘占用，结合`df -h`评估分区整体使用情况，指导清理策略。
- **配置生效与系统重启**：修改系统配置文件后，通过`systemctl reload`或`reboot`使更改生效。
- **GPU资源调度**：在模型训练或推理过程中，使用`gpustat -i`或`nvidia-smi`实时掌握GPU使用率、显存占用，避免资源冲突。
- **远程运维基础**：所有命令均可在SSH会话中直接执行，是[[concepts/远程开发技巧|远程开发技巧]]的核心支撑。

## 来源提及

- "useradd -m 用户名 # 创建用户" — [[一些常用命令|一些常用命令]]
- "du -h -x --max-depth=1 # 查看当前文件夹下的各个文件夹所占内存" — [[一些常用命令|一些常用命令]]
- "gpustat -i # 实时监视GPU使用情况(删去-i就不实时)" — [[一些常用命令|一些常用命令]]
- "chown -R liuhai:liuhai /opt # 将目录/opt 及其下面的所有文件、子目录的文件主改成 liuhai" — [[一些常用命令|一些常用命令]]
- "gpustat -i # 实时监视GPU使用情况" — [[一些常用命令|一些常用命令]]