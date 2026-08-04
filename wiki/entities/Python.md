---

type: entity
created: 2026-08-04
updated: 2026-08-04
sources: ["[[sources/一些常用命令_c2949b]]"]
tags: [product]
aliases:
  - "Python编程语言"
  - "Python 3"
  - "CPython"
sources:
  - [[sources/一些常用命令_c2949b]]
generation_complete: true
---


# Python

## 描述

Python 是一种解释型、面向对象的高级编程语言。它在本知识库中作为基础设施语言广泛出现：使用 [[entities/conda|conda]] / [[entities/mamba|mamba]] 管理环境时可以指定 Python 版本，通过 [[entities/pip|pip]] 安装和管理第三方包，在 [[concepts/远程开发|远程开发]] 场景中借助 [[entities/Jupyter-Notebook|Jupyter]] 运行 Python 代码，并利用 PyTorch 等库进行 GPU 计算。Python 生态的统一性使得这些工具能够协同工作，是许多 [[concepts/CLI命令|CLI命令]] 和自动化任务的底层依赖。

## 相关实体

- [[entities/conda|conda]]
- [[entities/mamba|mamba]]
- [[entities/pip|pip]]
- [[entities/Jupyter-Notebook|Jupyter-Notebook]]

## 相关概念

_无_

## 来源提及

- "conda create --name xxxx python=xxxx #创建新的虚拟环境" — [[一些常用命令_c2949b|一些常用命令_c2949b]]
- "mamba create -n py_310 python=3.10 # 创建新环境: -n 自定义名称 python=版本号" — [[一些常用命令_c2949b|一些常用命令_c2949b]]
- "``pip list --format=freeze > requirements.txt ``" — [[一些常用命令_c2949b|一些常用命令_c2949b]]