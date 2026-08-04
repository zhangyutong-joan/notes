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
  - "My Structured Query Language"
  - "MySQL 数据库"
  - "关系型数据库管理系统"
---

## 描述
MySQL 是一个开源的关系型数据库管理系统（RDBMS），使用 [[concepts/sql|结构化查询语言（SQL）]] 进行数据定义、操作和查询。它以其可靠性、高性能和易用性著称，被广泛部署在 [[concepts/web-application|Web 应用]]、企业系统、数据仓库以及嵌入式场景中。MySQL 采用客户端/服务器架构，支持多线程、多用户访问，并提供丰富的事务与存储引擎支持（如 InnoDB）。在 Windows 环境下，通常通过 `services.msc` 服务管理工具对 MySQL 服务进行控制；源文件 [[sources/一些常用命令_c2949b]] 中推荐不设为开机自启，而是需要时手动启动以节省系统资源。作为 LAMP/LEMP 堆栈的核心组件之一，MySQL 已成为世界上最流行的开源数据库。参考《一些常用命令》笔记中的详细操作指引，通过按 Win+R 打开运行对话框，输入 `services.msc` 并回车，然后在服务列表中找到 MySQL 服务并右键“启动”，即可实现按需启动，这种配置方式在本地开发环境中尤为常见。

## 相关实体
- [[entities/maria-db|MariaDB]]

## 相关概念
- [[concepts/rdbms|关系型数据库]]
- [[concepts/sql|结构化查询语言（SQL）]]
- [[concepts/open-source|开源软件]]
- [[concepts/dbms|数据库管理系统]]
- [[concepts/web-application|Web 应用]]

## 源文件引用
> “在 Windows 系统中，MySQL 服务的启动方式建议不要开机自启，而是通过 `services.msc` 服务管理工具手动启动：右键点击 MySQL 服务选择‘启动’。这种方法可以节省系统资源，并提供按需启动的灵活性。”
> — [[sources/一些常用命令_c2949b]]

## 来源提及

- "对于MySQL是否开机自启，建议手动启动，需要时Win + R 打开“运行”对话框，输入services.msc，点击确定或直接Enter键，进入"服务"管理器窗口，找到MySQL，右键“启动”就好。" (对于MySQL是否开机自启，建议手动启动，需要时按Win+R打开“运行”对话框，输入services.msc并确定，进入“服务”管理器窗口，找到MySQL服务，右键选择“启动”即可。) — [[一些常用命令|一些常用命令]]
- "对于MySQL是否开机自启，建议手动启动，需要时Win + R 打开“运行”对话框，输入services.msc，点击确定或直接Enter键，进入“服务”管理器窗口，找到MySQL，右键“启动”就好。" — [[一些常用命令|一些常用命令]]