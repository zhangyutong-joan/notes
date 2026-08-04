---

type: concept
created: 2026-08-04
updated: 2026-08-04
sources: ["[[sources/module-集群命令_3bd63b]]"]
tags: [method]
aliases:
  - "模块加载"
  - "环境模块加载"
  - "environment module load"
sources:
  - [[sources/module-集群命令_3bd63b]]
generation_complete: true
---


# module load

## 定义
`module load` 是环境模块系统（Environment Modules 或 Lmod）提供的核心命令，用于在 HPC 集群或计算环境中动态加载指定软件模块。执行该命令后，系统会自动修改当前 shell 会话的环境变量（如 `PATH`、`LD_LIBRARY_PATH`、`MANPATH` 等），使目标软件及其依赖立即可用。源文件中通过 `module load anaconda3` 加载 Anaconda 发行版，从而启用 conda 及其生态工具，体现了在共享集群上为多用户、多版本软件提供隔离与即时切换的标准方法。

## 关键特征
- **动态会话级变更**：环境变量修改仅作用于当前 shell，不影响其他用户或后续登录会话，避免持久性冲突。  
- **多版本管理**：同一软件的多个版本可共存，用户通过 `module load app/version` 按需选择，无需手动维护路径。  
- **依赖自动解析**：模块系统通常能自动加载目标模块所依赖的其他模块，简化复杂软件栈的部署。  
- **可逆操作**：对应 `module unload` 命令可干净地移除已加载模块，恢复未加载前的环境。  
- **跨调度器与集群通用**：广泛适配 SLURM、PBS 等作业调度系统，是高性能计算领域的标准环境管理方式。

## 应用
- **计算集群基础环境准备**：在登录节点或作业脚本中加载编译器（GCC、Intel）、MPI 库、数学库等，为上层应用提供构建和运行环境。  
- **Python 与数据科学工具链**：通过 `module load anaconda3` 使 conda 环境可用，进而激活 `py310_torch112_cu116` 等预配置的虚拟环境，快速启用 PyTorch、CUDA 深度学习框架。  
- **作业调度脚本集成**：在 SLURM 脚本头通过 `#SBATCH` 配合 `module load` 语句，确保计算节点自动获得一致的软件栈，实现可复现的高通量计算。  
- **教学与多租户场景**：允许多个用户在同一集群上使用不同的 Python、R、MATLAB 版本，互不干扰，降低维护成本。

## 相关概念
- [[concepts/环境管理|环境管理]]  
- [[concepts/Linux命令|Linux命令]]  
- [[concepts/conda命令|conda命令]]  
- [[concepts/远程开发|远程开发]]

## 相关实体
- [[entities/conda|conda]]  
- [[entities/py310_torch112_cu116]]

## 源文件引用
在 [[sources/module-集群命令_3bd63b]] 中，展示了通过 `module load anaconda3` 命令为当前会话激活 Anaconda 环境，随后 conda 及相关工具便成为可直接使用的命令行工具。这一操作正是 `module load` 在 HPC 环境中作为软件接入入口的典型实践。

## 来源提及

- "module load anaconda3" — [[module 集群命令|module 集群命令]]
- "每次使用cmd首先做：" — [[module 集群命令|module 集群命令]]