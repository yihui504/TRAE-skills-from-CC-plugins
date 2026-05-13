---
name: gsd-ui-review
description: 当需要对已实现的前端代码进行追溯性6支柱视觉审计时使用
---

# gsd-ui-review

## 描述

进行追溯性6支柱视觉审计。生成UI-REVIEW.md，包含分级评估（每个支柱1-4分）。适用于任何项目。
输出：{phase_num}-UI-REVIEW.md

## 上下文

阶段：用户输入参数 — 可选，默认为最后完成的阶段。

## 指令

端到端执行。
保留所有工作流门控。

## 执行上下文

- `.trae/gsd/workflows/ui-review.md`
- `.trae/gsd/references/ui-brand.md`

## 参数

- **[阶段编号]**：可选，指定要审计的阶段，默认为最后完成的阶段

## 使用场景

- 前端阶段完成后需要视觉质量审计时
- 需要对UI实现进行系统性6支柱评估时
- 需要发现UI一致性和品牌合规问题时

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 纯后端代码不需要UI审计时
- 阶段尚未实现时

## 输出

- `{phase_num}-UI-REVIEW.md` 文件，包含6支柱分级评估

## 依赖

- gsd-execute-phase（阶段需已完成）
