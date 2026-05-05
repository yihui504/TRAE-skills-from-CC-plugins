---
name: ultrawork
description: Use when facing 2+ independent tasks that can be worked on without shared state or sequential dependencies. Parallel execution engine for high-throughput task completion.
---

# Ultrawork

## 描述

Ultrawork是并行执行引擎，用于独立工作的高吞吐量任务完成。它强调意图明确、并行上下文收集、依赖感知的任务图，以及简洁的基于证据的执行摘要。

## 使用场景

- 多个独立任务可以同时运行
- 用户说 "ultrawork"、"ulw"、或想要并行执行
- 需要同时将工作委派给多个子代理
- 任务受益于并发执行，但用户会自行管理完成

## 不适用场景

- 只有一个顺序任务，没有并行机会 → 直接委派给执行代理
- 任务需要保证完成并带验证 → 使用 ralph（ralph包含ultrawork）
- 任务需要完整的自主管道 → 使用 autopilot（autopilot包含ralph，ralph包含ultrawork）

## 指令

### 1. 明确意图

确认请求是以下哪种类型：
- **实现**：编写代码
- **调查**：搜索/分析
- **评估**：审查/检查
- **研究**：探索/学习

在明确之前不要开始编码。

### 2. 并行收集上下文

- 使用直接工具进行快速读取/搜索
- 使用 Task 子代理进行广泛的上下文探索

### 3. 分类任务独立性

识别哪些任务可以并行运行，哪些有依赖关系。

### 4. 为非平凡工作创建任务图

- 并行执行波次
- 依赖矩阵
- 每个任务的验收标准和验证步骤

### 5. 路由到正确的子代理类型

| 任务复杂度 | Task subagent_type | 用途 |
|-----------|-------------------|------|
| 简单查找/定义 | search | 文件枚举、模式计数、简单查找 |
| 标准实现 | backend-architect 或 frontend-architect | 代码分析、模式检测、标准开发 |
| 复杂分析/推理 | backend-architect | 架构分析、跨领域关注、假设验证 |

### 6. 同时发射独立任务

所有并行安全的任务一次性发射：

```
Task(subagent_type="backend-architect", query="Add missing type export for Config interface")
Task(subagent_type="frontend-architect", query="Implement the /api/users endpoint with validation")
Task(subagent_type="search", query="Find all test files related to auth middleware")
```

### 7. 顺序运行依赖任务

等待前置条件完成后再启动依赖工作。

### 8. 后台运行长操作

构建、安装和测试套件使用 `blocking: false`：

```
RunCommand(command="npm install && npm run build", blocking=false, requires_approval=false)
```

### 9. 验证完成

所有任务完成后进行轻量验证：
- [ ] 构建/类型检查通过
- [ ] 受影响的测试通过
- [ ] 没有引入新错误

## 与其他模式的关系

```
ralph (持久化包装器)
 └─ 包含: ultrawork (本技能)
     └─ 提供: 仅并行执行

autopilot (自主执行)
 └─ 包含: ralph
     └─ 包含: ultrawork (本技能)
```

Ultrawork是并行层。Ralph添加持久化和验证。Autopilot添加完整的生命周期管道。

## 注意事项

- 当ultrawork被直接调用（非通过ralph），仅应用轻量验证
- 如果任务在重试中反复失败，报告问题而不是无限重试
- 当任务有不清楚的依赖或冲突需求时，升级给用户
- 委派任务时始终明确指定 `subagent_type` 参数
