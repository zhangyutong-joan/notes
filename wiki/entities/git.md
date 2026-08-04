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
  - "Git"
---

# git

## 描述
Git 是一个分布式版本控制系统，用于跟踪代码文件的变更，支持多人协作开发。源文件[[sources/一些常用命令_c2949b]] 中记录了 Git 的日常操作命令，包括仓库克隆、远程仓库关联、暂存与提交、推送与拉取、分支管理以及全局配置等。该文档还提供了 fork 仓库后保持与上游同步的步骤，以及通过 Git 设置 HTTP 代理和跳过 SSL 证书校验的全局配置命令。Git 是软件开发流程中不可或缺的工具，覆盖了从个人练习到团队协作维护的常见场景。

## 相关实体
- [[entities/conda|conda]]
- [[entities/mamba|mamba]]
- [[entities/MATLAB|MATLAB]]

## 相关概念
- [[concepts/版本控制|版本控制]]
- [[concepts/代理配置|代理配置]]

## 来源提及

- "git add <file name> # 将文件放到暂存区" — [[一些常用命令|一些常用命令]]
- "git commit -m "注释" # 将暂存区提交到本地仓库" — [[一些常用命令|一些常用命令]]
- "git push <仓库别名> # 将本地仓库推送到远程仓库" — [[一些常用命令|一些常用命令]]
- "git config --global http.proxy "http://127.0.0.1:梯子端口号"" — [[一些常用命令|一些常用命令]]
- "git remote add origin https://github.com/zyt1998/xxx.git # 添加远程仓库" — [[一些常用命令_c2949b|一些常用命令_c2949b]]
- "git clone https://github.com/zyt1998/xxx.git # 克隆远程仓库" — [[一些常用命令_c2949b|一些常用命令_c2949b]]