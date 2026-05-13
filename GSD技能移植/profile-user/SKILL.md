---
name: gsd-profile-user
description: 当需要生成开发者行为画像并创建可发现的配置产物时使用
---

# gsd-profile-user

## 描述

从会话分析（或问卷）生成开发者行为画像，并产出产物（USER-PROFILE.md、/gsd-dev-preferences、CLAUDE.md部分），用于个性化响应。

路由到profile-user工作流，该工作流编排完整流程：同意门控、会话分析或问卷回退、画像生成、结果展示和产物选择。

## 上下文

来自用户输入参数的标志：
- `--questionnaire` — 完全跳过会话分析，仅使用问卷路径
- `--refresh` — 即使已有画像也重新构建，备份旧画像，显示维度差异

## 指令

端到端执行profile-user工作流。

工作流处理所有逻辑，包括：
1. 初始化和已有画像检测
2. 会话分析前的同意门控
3. 会话扫描和数据充分性检查
4. 会话分析（画像代理）或问卷回退
5. 跨项目分割解决
6. 画像写入USER-PROFILE.md
7. 结果展示（含报告卡和亮点）
8. 产物选择（dev-preferences、CLAUDE.md部分）
9. 顺序产物生成
10. 带刷新差异的摘要（如适用）

## 执行上下文

- `.trae/gsd/workflows/profile-user.md`
- `.trae/gsd/references/ui-brand.md`

## 参数

- `--questionnaire`：跳过会话分析，仅使用问卷
- `--refresh`：重新构建已有画像

## 使用场景

- 需要生成开发者行为画像以个性化AI响应
- 首次使用GSD需要建立偏好配置
- 需要更新已有的开发者画像

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 不需要个性化AI响应
- 不愿意分享会话数据用于分析
- 仅需查看项目配置

## 输出

- USER-PROFILE.md
- dev-preferences配置
- CLAUDE.md部分（可选）

## 依赖

- 需要足够的会话历史用于分析（或使用--questionnaire替代）
