---
name: autopilot
description: Use when you want full autonomous execution from idea to working code. Say "autopilot", "auto pilot", "build me", "create me", "make me", or "full auto" for hands-off multi-phase development.
---

# Autopilot

## 描述

Autopilot接收一个简短的产品想法，自主处理完整生命周期：需求分析、技术设计、规划、并行实现、QA循环和多视角验证。从2-3行描述产出可工作的、经过验证的代码。

## 使用场景

- 用户想要从想法到可工作代码的端到端自主执行
- 用户说 "autopilot"、"auto pilot"、"autonomous"、"build me"、"create me"、"make me"、"full auto"、"handle it all"、"I want a/an..."
- 任务需要多个阶段：规划、编码、测试和验证
- 用户想要放手执行，愿意让系统运行到完成

## 不适用场景

- 用户想要探索选项或头脑风暴 → 使用 omc-plan
- 用户说 "just explain"、"draft only"、"what would you suggest" → 对话式回答
- 用户想要单一聚焦的代码变更 → 使用 ralph 或直接委派
- 用户想要审查或批评现有计划 → 使用 omc-plan --review
- 快速修复或小bug → 直接委派

## 指令

### Phase 0 - 扩展

将用户的想法转化为详细规格说明。

- **如果存在共识计划**（`.trae/plans/consensus-*.md`）：跳过Phase 0和Phase 1，直接进入Phase 2
- **如果存在深度访谈规格**（`.trae/specs/deep-interview-*.md`）：使用预验证的规格作为Phase 0输出
- **如果输入模糊**（无文件路径、函数名或具体锚点）：建议先使用 deep-interview 技能
- **否则**：使用 Task 工具派遣 `backend-architect` 子代理提取需求并创建技术规格

输出：`.trae/autopilot/spec.md`

### Phase 1 - 规划

从规格创建实现计划。

- **如果存在共识计划**：跳过——已在3阶段管道中完成
- 使用 Task 工具派遣 `backend-architect` 子代理创建计划
- 使用 Task 工具派遣 `backend-architect` 子代理验证计划

输出：`.trae/plans/autopilot-impl.md`

### Phase 2 - 执行

使用 ralph + ultrawork 实现计划。

按任务复杂度路由：
- 简单任务 → `search` 或 `backend-architect`
- 标准任务 → `backend-architect` 或 `frontend-architect`
- 复杂任务 → `backend-architect`

独立任务并行运行。

### Phase 3 - QA

循环直到所有测试通过（UltraQA模式）。

- 构建、lint、测试、修复失败
- 最多重复5个循环
- 如果同一错误重复3次则提前停止（表明是根本问题）

### Phase 4 - 验证

并行多视角审查：

- 使用 `backend-architect`：功能完整性
- 使用 `backend-architect`（带安全审查指令）：漏洞检查
- 使用 `backend-architect`（带质量审查指令）：质量审查

所有审查必须通过；被拒绝的项修复后重新验证。

### Phase 5 - 清理

成功完成后删除所有状态文件：
- 删除 `.trae/state/autopilot-state.json`
- 删除 `.trae/state/ralph-state.json`
- 删除 `.trae/prd.json`（可选，保留用于参考）
- 向用户报告完成摘要

## 子代理路由映射

| OMC原始类型 | Trae Solo替代 | 用途 |
|------------|--------------|------|
| architect | backend-architect | 架构设计和技术规格 |
| critic | backend-architect（带审查指令） | 计划和代码审查 |
| executor (haiku) | search | 简单查找和枚举 |
| executor (sonnet) | backend-architect / frontend-architect | 标准实现 |
| executor (opus) | backend-architect | 复杂分析和实现 |
| security-reviewer | backend-architect（带安全审查指令） | 安全审查 |
| code-reviewer | backend-architect（带质量审查指令） | 代码质量审查 |

## 状态管理

使用文件系统管理状态：

- **Autopilot状态**：`.trae/state/autopilot-state.json`
- **规格文件**：`.trae/autopilot/spec.md`
- **计划文件**：`.trae/plans/autopilot-impl.md`

autopilot-state.json格式：
```json
{
  "active": true,
  "phase": 2,
  "started_at": "2026-05-04T12:00:00Z",
  "spec_path": ".trae/autopilot/spec.md",
  "plan_path": ".trae/plans/autopilot-impl.md"
}
```

## 执行策略

- 每个阶段必须完成后才开始下一个
- 在阶段内尽可能使用并行执行（Phase 2和Phase 4）
- QA循环最多5次；同一错误持续3次则停止并报告根本问题
- 验证需要所有审查者通过；被拒绝的项修复后重新验证
- 任何时候用户说 "stop" 或 "cancel" 都可取消

## 恢复

如果autopilot被取消或失败，再次运行 `autopilot` 从停止处恢复。读取 `.trae/state/autopilot-state.json` 确定当前阶段。

## 输入最佳实践

1. 明确领域——"bookstore" 而非 "store"
2. 提及关键特性——"with CRUD"、"with authentication"
3. 指定约束——"using TypeScript"、"with PostgreSQL"
4. 让它运行——除非真正需要，避免中断

## 完成检查清单

- [ ] 所有5个阶段完成（扩展、规划、执行、QA、验证）
- [ ] Phase 4中所有审查者通过
- [ ] 测试通过（用新鲜测试运行输出验证）
- [ ] 构建成功（用新鲜构建输出验证）
- [ ] 状态文件已清理
- [ ] 用户被告知完成，附构建内容摘要
