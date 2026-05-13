---
name: gsd-resume-work
description: 当需要从上次会话恢复工作并完整还原上下文时使用
---

# gsd-resume-work

## 描述

从上次会话恢复完整项目上下文并无缝继续工作。

路由到resume-project工作流，处理：
- STATE.md加载（如果缺失则重建）
- 检查点检测（.continue-here文件）
- 未完成工作检测（有PLAN但没有SUMMARY）
- 状态展示
- 上下文感知的下一步操作路由

## 上下文

无需额外参数，自动检测项目状态。

## 指令

端到端执行。

## 执行上下文

- `.trae/gsd/workflows/resume-project.md`

## 使用场景

- 新会话开始时需要恢复之前的工作上下文
- 项目有未完成的阶段需要继续时
- 需要了解项目当前状态并确定下一步操作时

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 全新项目初始化时（应使用new-project）
- 需要查看项目统计信息时（应使用stats）

## 输出

- 项目状态报告（控制台输出）
- 上下文恢复后的下一步操作建议

## 依赖

- gsd-execute-phase（可能路由到）
- gsd-plan-phase（可能路由到）
