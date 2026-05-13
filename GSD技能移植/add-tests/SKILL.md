---
name: gsd-add-tests
description: 当需要为已完成的阶段生成单元测试和E2E测试时使用
---

# gsd-add-tests

## 描述

为已完成的阶段生成单元和E2E测试，使用其SUMMARY.md、CONTEXT.md和VERIFICATION.md作为规格说明。

分析实现文件，将其分类为TDD（单元）、E2E（浏览器）或Skip类别，向用户展示测试计划以供批准，然后按照RED-GREEN约定生成测试。

输出：测试文件以 `test(phase-{N}): add unit and E2E tests from add-tests command` 消息提交。

## 上下文

阶段：用户输入参数

- `.trae/gsd/planning/STATE.md`
- `.trae/gsd/planning/ROADMAP.md`

## 指令

端到端执行。
保留所有工作流关卡（分类批准、测试计划批准、RED-GREEN验证、差距报告）。

## 执行上下文

- `.trae/gsd/workflows/add-tests.md`

## 参数

- `<phase>` — 阶段编号（整数、小数或字母后缀）
- `[additional instructions]` — 可选的额外指令

示例：`gsd-add-tests 12`
示例：`gsd-add-tests 12 focus on edge cases in the pricing module`

## 使用场景

- 阶段实现完成后需要补充测试覆盖
- 需要根据UAT标准和验证文档生成测试
- 需要系统化地对阶段产出进行TDD和E2E测试

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 阶段尚未完成实现时
- 需要先修复bug再写测试时（应先使用debug skill）
- 只需要快速验证一个简单改动时（应使用fast skill）

## 输出

- 测试文件（单元测试和E2E测试）
- 提交记录：`test(phase-{N}): add unit and E2E tests from add-tests command`

## 依赖

- gsd-execute-phase（阶段需先完成执行）
- gsd-verify-work（验证文档作为测试规格来源）
