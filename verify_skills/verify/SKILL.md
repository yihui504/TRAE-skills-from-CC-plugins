---
name: verify
description: Verify that a change really works before you claim completion. Use when the user wants confidence that a feature, fix, or refactor actually works.
---

# Verify

## 描述

当用户想要确认一个功能、修复或重构确实有效时，使用此技能。

目标：将模糊的"应该可以工作"的声明转化为具体证据。

## 使用场景

- 用户说 "verify"、"check this works"、"make sure it's correct"
- 完成功能实现后需要验证
- 修复 bug 后需要确认修复有效
- 重构后需要确认行为未改变
- 在声称工作完成之前需要证据

## 指令

1. 识别必须证明的确切行为
2. 优先使用现有测试
3. 如果覆盖缺失，运行可用的最窄直接验证命令
4. 如果直接自动化不够，描述手动验证步骤并收集具体可观察证据
5. 仅报告实际验证的内容

### 验证顺序

1. 现有测试
2. 类型检查 / 构建
3. 窄范围直接命令检查
4. 手动或交互式验证

### 规则

- 没有证据不要说变更已完成
- 如果检查失败，明确包含失败信息
- 如果没有现实的验证路径，明确说明而不是虚张声势
- 优先使用简洁的证据摘要而非嘈杂的日志

## 示例

**输出格式：**
- 验证了什么
- 运行了哪些命令/测试
- 通过了什么
- 失败了什么或仍未验证