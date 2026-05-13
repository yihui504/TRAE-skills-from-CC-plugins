---
name: gsd-pr-branch
description: 当需要创建干净的PR分支时使用——过滤掉规划目录的提交，准备代码审查
---

# gsd-pr-branch

## 描述

通过过滤掉当前分支中的`.trae/gsd/planning/`提交，创建适合拉取请求的干净分支。审查者只看到代码变更，而非GSD规划产物。

这解决了PR差异被PLAN.md、SUMMARY.md、STATE.md变更（与代码审查无关）充斥的问题。

## 上下文

无特殊上下文要求。

## 指令

端到端执行。

## 执行上下文

- `.trae/gsd/workflows/pr-branch.md`

## 参数

- `[target branch]`：目标分支（默认：main）

## 使用场景

- 需要创建不含GSD规划产物的干净PR分支
- PR差异被规划文件变更充斥
- 需要为代码审查准备干净的分支

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 不使用Git的项目
- 不需要创建PR
- 分支中没有规划文件提交

## 输出

- 干净的PR分支（过滤掉.trae/gsd/planning/提交）

## 依赖

- 需要Git仓库
