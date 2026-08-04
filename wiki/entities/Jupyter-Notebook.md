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
  - "Jupyter"
  - "交互式笔记本"
---

# Jupyter Notebook

## 描述
Jupyter Notebook 是一个开源的 Web 应用程序，允许用户创建和共享包含实时代码、方程、可视化和叙述文本的文档。它基于 IPython 构建，提供交互式编程体验，支持 Python 等多种编程语言，在数据科学和机器学习领域得到广泛应用。在源文件 [[sources/一些常用命令_c2949b]] 中记录了如何远程启动该服务：终端执行 `jupyter notebook --allow-root`，然后复制带 token 的 URL 到浏览器访问，体现了其对于远程开发场景的便利性。这种访问方式依赖 [[concepts/jupyter-notebook-remote-access|Jupyter Notebook远程访问]] 的典型配置，使探索性数据分析与教学演示变得更加灵活。

## 相关实体
暂无

- [[entities/python|Python]]
- [[entities/nvidia-gpu|NVIDIA GPU]]
## 相关概念
- [[concepts/jupyter-notebook-remote-access|Jupyter Notebook远程访问]]

## 来源提及

- "开启jupyter直接在终端输入 ``jupyter notebook --allow-root``然后复制terminal下的“Jupyter Notebook 6.3.0 is running at:”下面的链接到浏览器就可以了。" (开启Jupyter直接在终端输入 ``jupyter notebook --allow-root``，然后复制终端中“Jupyter Notebook 6.3.0 is running at:”下面的链接到浏览器即可。) — [[一些常用命令|一些常用命令]]