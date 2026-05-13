---
name: gsd-inbox
description: 当需要分类审查GitHub issues和PRs是否符合项目模板和贡献指南时使用
---

# gsd-inbox

## 描述

一键分类项目的GitHub收件箱。获取所有开放的issues和PRs，根据对应的模板要求（feature、enhancement、bug、chore、fix PR、enhancement PR、feature PR）逐一审查，报告完整性和合规性，并可选地应用标签或关闭不合规的提交。

**流程：** 检测仓库 → 获取开放的issues + PRs → 按类型分类 → 对照模板审查 → 报告发现 → 可选操作（标签、评论、关闭）

## 上下文

**参数：**
- `--issues` — 仅审查issues（跳过PRs）
- `--prs` — 仅审查PRs（跳过issues）
- `--label` — 审查后自动应用推荐标签
- `--close-incomplete` — 关闭不符合模板合规性的issues/PRs（附说明原因的评论）
- `--repo owner/repo` — 覆盖自动检测的仓库（默认为当前git远程仓库）

## 指令

端到端执行。
从参数中解析标志并传递给工作流。

## 执行上下文

- `.trae/gsd/workflows/inbox.md`

## 参数

- `--issues`：仅审查issues
- `--prs`：仅审查PRs
- `--label`：自动应用推荐标签
- `--close-incomplete`：关闭不合规的提交
- `--repo owner/repo`：指定仓库

## 使用场景

- 需要批量审查GitHub issues和PRs的合规性
- 需要为issues/PRs自动应用标签
- 需要清理不合规的提交

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 不使用GitHub的项目
- 仅需查看单个issue或PR
- 不涉及模板合规性审查的场景

## 输出

- 每个issue/PR的合规性报告
- 可选：应用的标签、关闭的提交

## 依赖

- 需要GitHub仓库访问权限
