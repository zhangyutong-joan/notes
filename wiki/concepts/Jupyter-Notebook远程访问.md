---

type: concept
created: 2026-08-04
updated: 2026-08-04
sources: ["[[sources/一些常用命令_c2949b]]"]
tags: [method]
aliases:
  - "远程Jupyter Notebook"
  - "Remote Jupyter Notebook"
  - "Jupyter远程访问"
sources:
  - [[sources/一些常用命令_c2949b]]
generation_complete: true
---


# Jupyter Notebook远程访问

## 定义
Jupyter Notebook远程访问是指在一台服务器上启动 Jupyter Notebook 服务，并通过网络在本地浏览器中访问和交互的方法。用户通过远程终端启动服务并获取包含 token 的 URL，随后将该 URL 粘贴到本地浏览器即可建立连接，实现对远程计算资源的交互式使用。

## 关键特征
- 无需远程桌面环境，仅通过浏览器即可使用远程计算资源
- 依赖 token 机制进行身份验证，保障连接安全性
- 常用于服务器、云端 GPU 工作站等无图形界面的环境
- 支持多用户通过不同端口或 token 同时访问
- 可结合 SSH 隧道、反向代理等方式增强安全性与灵活性

## 应用
- 在 GPU 云服务器上运行深度学习实验，并通过本地浏览器进行交互式调试
- 远程数据分析与可视化，利用服务器高性能处理器加速计算
- 教学场景中，教师可在服务器上搭建共享 Notebook 环境，学生远程访问
- 临时借调高性能硬件（如大内存服务器）完成本地机器无法胜任的任务

## 相关概念
- [[concepts/远程开发|远程开发]]
- [[concepts/远程开发技巧|远程开发技巧]]
- [[concepts/代理配置|代理配置]]（当需要通过代理访问远程服务器时）

## 相关实体
- [[entities/Jupyter-Notebook|Jupyter Notebook]]

## Mentions in Source
> 在远程终端执行 ``jupyter notebook --allow-root`` 命令启动服务，然后从终端输出中复制包含 token 的 URL，并将其粘贴到本地浏览器地址栏中即可连接。`--allow-root` 参数允许以 root 用户身份运行，实际生产环境中需谨慎使用。 — [[sources/一些常用命令_c2949b]]

## 来源提及

- "开启jupyter直接在终端输入 ``jupyter notebook --allow-root``然后复制terminal下的“Jupyter Notebook 6.3.0 is running at:”下面的链接到浏览器就可以了。" (开启Jupyter直接在终端输入 ``jupyter notebook --allow-root``，然后复制终端中“Jupyter Notebook 6.3.0 is running at:”下面的链接到浏览器即可。) — [[一些常用命令|一些常用命令]]