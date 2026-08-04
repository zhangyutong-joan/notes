---

type: concept
created: 2026-08-04
updated: 2026-08-04
sources: ["[[sources/一些常用命令_c2949b]]"]
tags: [method]
aliases:
  - "Fork后同步上游"
  - "保持Fork仓库同步"
  - "同步Fork"
sources:
  - [[sources/一些常用命令_c2949b]]
generation_complete: true
---


# git fork同步更新

## 定义
Git Fork同步更新是一套在 GitHub（或类似平台）上使用的 Git 操作流程，用于将已 fork 的仓库与原始上游仓库保持代码同步。该过程通过从上游获取更新、合并到本地分支并推送至自己的远程 fork 仓库，确保 fork 的代码与上游主分支一致，从而为后续协作与贡献奠定基础。

## 关键特征
- **上游注册**：通常需要先将原始仓库添加为名为 `upstream` 的远程地址
- **获取更新**：使用 `git fetch upstream` 将上游仓库的最新提交拉取到本地
- **切换分支**：切换到主分支（如 `main` 或 `master`）
- **合并更新**：执行 `git merge upstream/main` 将上游的更新合并进当前分支
- **推送同步**：通过 `git push origin main` 将合并后的代码推送到自己的 fork 仓库
- **冲突处理**：若出现合并冲突，需手动解决后再提交和推送
- **持续维护**：该流程可反复执行，使 fork 仓库长期与原始项目保持同步

## 应用
- 在开源协作中，贡献者需要基于最新版本的原始仓库进行开发，因此定期同步 fork 是基础操作
- 当原始项目修复重要漏洞或发布新功能时，通过此操作快速将改进合并到自己的环境
- 避免因 fork 与上游差异过大导致未来 Pull Request 难以合并

## 相关概念
- [[concepts/版本控制|版本控制]]
- [[concepts/git命令|git命令]]

## 相关实体
- [[entities/git|git]]

## 来源提及

- "git fetch upstream # 胡拉取远程仓库的更新" — [[一些常用命令|一些常用命令]]
- "git merge upstream/main # 合并远程仓库的更新到本地仓库" — [[一些常用命令|一些常用命令]]
- "git push origin main # 将本地仓库的更新推送到远程fork的仓库" — [[一些常用命令|一些常用命令]]