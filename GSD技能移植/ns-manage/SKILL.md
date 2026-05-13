---
name: gsd-ns-manage
description: 当需要路由到管理相关skill时使用——配置、工作区、工作流、收件箱
---

# gsd-ns-manage

## 描述

根据用户意图路由到适当的管理skill。
`gsd-config`（设置+高级+集成+配置文件）和`gsd-workspace`（新建+列表+移除）是合并后的条目。

| 用户意图 | 调用 |
|---|---|
| 配置GSD设置（基础/高级/集成/配置文件） | gsd-config |
| 管理工作区（创建/列表/移除） | gsd-workspace |
| 管理并行工作流 | gsd-workstreams |
| 在新的上下文线程中继续工作 | gsd-thread |
| 暂停当前工作 | gsd-pause-work |
| 恢复暂停的工作 | gsd-resume-work |
| 更新GSD安装 | gsd-update |
| 发布已完成的工作 | gsd-ship |
| 处理收件箱项 | gsd-inbox |
| 创建干净的PR分支 | gsd-pr-branch |
| 撤销上一次GSD操作 | gsd-undo |

使用Skill工具直接调用匹配的skill。

## 上下文

无特殊上下文要求。根据用户意图选择对应的skill。

## 指令

根据用户意图，使用Skill工具直接调用匹配的skill。

## 使用场景

- 用户需要配置GSD设置或管理工作区
- 用户需要暂停/恢复工作或管理工作流
- 用户需要处理收件箱或创建PR分支

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 用户已明确指定要使用的具体skill
- 不涉及管理类的需求

## 输出

路由到对应的skill，产出取决于被调用的skill。

## 依赖

- gsd-config
- gsd-workspace
- gsd-workstreams
- gsd-thread
- gsd-pause-work
- gsd-resume-work
- gsd-update
- gsd-ship
- gsd-inbox
- gsd-pr-branch
- gsd-undo
