---

type: concept
created: 2026-08-04
updated: 2026-08-04
sources: ["[[sources/一些常用命令_c2949b]]"]
tags: [method]
aliases:
  - "Git常用操作"
  - "Git版本控制"
  - "Git Commands"
sources:
  - [[sources/一些常用命令_c2949b]]
generation_complete: true
---


# git命令

## 定义
git命令是围绕Git分布式版本控制系统而设计的一套终端操作指令，覆盖了从本地仓库初始化、文件暂存与提交、远程仓库同步到分支管理等完整的版本控制工作流。这些命令是团队协作与代码管理的基础，也是现代软件工程中版本控制不可或缺的实用技能。

## 关键特征
- 覆盖完整的 Git 工作流：`git add`（暂存）、`git commit`（提交）、`git push`/`git pull`（推送/拉取）
- 支持远程仓库管理，包括 `git remote add`、`git remote remove` 以及 `git clone`
- 提供分支查看与切换能力，常用命令为 `git branch` 及相关参数
- 可对文件/文件夹进行缓存删除，如 `git rm --cached` 等操作
- 命令组合灵活，适应个人开发与团队协作等多种场景

## 应用
- **日常代码提交**：通过 `git add` + `git commit` + `git push` 将本地修改同步到远程仓库，实现版本记录
- **协作开发**：利用 `git pull` 拉取远程更新，`git branch` 管理并行开发分支，合并后推送
- **仓库克隆与初始化**：使用 `git clone` 复制现有仓库，或 `git init` 新建本地仓库
- **缓存清理**：当需要停止跟踪某些文件时，使用 `git rm --cached` 解除版本控制但保留本地文件
- **远程仓库配置**：通过 `git remote add` 链接多个远程仓库，便于备份或协作

## 相关概念
- [[concepts/Linux命令|Linux命令]]：许多 git 命令在 Linux 终端中执行，与 Linux 命令行环境紧密相关
- [[concepts/版本控制|版本控制]]：git命令是版本控制理念的具体实现
- [[concepts/git fork同步更新|git fork同步更新]]：涉及从上游仓库同步更新 fork 仓库的命令操作
- [[concepts/远程开发技巧|远程开发技巧]]：远程仓库管理是远程开发的基础环节

## 相关实体
暂无直接相关的实体。

## 来源提及

- "git add <file name> # 将文件放到暂存区" — [[一些常用命令|一些常用命令]]
- "git commit -m "注释" # 将暂存区提交到本地仓库" — [[一些常用命令|一些常用命令]]
- "git push <仓库别名> # 将本地仓库推送到远程仓库" — [[一些常用命令|一些常用命令]]
- "git branch # 显示你的仓库的所有本地分支，星号分支是您当前的分支。" — [[一些常用命令|一些常用命令]]