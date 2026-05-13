---
name: gsd-plan-phase
description: 当需要创建详细的阶段计划PLAN.md并进行验证循环时使用
---

# gsd-plan-phase

## 描述

为路线图阶段创建可执行的计划提示（PLAN.md文件），集成研究和验证。

**默认流程：** 研究（如需要） → 规划 → 验证 → 完成

**仅研究模式（`--research-phase <N>`）：** 为阶段`N`生成`gsd-phase-researcher`，写入`RESEARCH.md`，然后在规划器运行之前退出。适用于跨阶段研究、在承诺规划方法之前审查文档，以及仅迭代研究的修正循环（比重新生成规划器便宜得多）。替代已删除的`/gsd-research-phase`命令。

**仅研究修饰符：**
- **无标志** — 当`RESEARCH.md`已存在时，提示用户选择`update / view / skip`。
- **`--research`** — 强制刷新：无条件重新生成研究者，不提示。跳过已有RESEARCH.md菜单。
- **`--view`** — 仅查看：将已有`RESEARCH.md`打印到stdout。不生成研究者。修正循环中最便宜的模式。如果尚无`RESEARCH.md`，报错并提示去掉`--view`。

**编排器角色：** 解析参数，验证阶段，研究领域（除非跳过），生成gsd-planner，用gsd-plan-checker验证，迭代直到通过或达到最大迭代次数，展示结果。

## 上下文

阶段编号：用户输入参数（可选——如省略自动检测下一个未规划阶段）

**参数：**
- `--research` — 即使RESEARCH.md已存在也强制重新研究
- `--skip-research` — 跳过研究，直接进入规划
- `--gaps` — 差距闭合模式（读取VERIFICATION.md，跳过研究）
- `--skip-verify` — 跳过验证循环
- `--prd <file>` — 使用PRD/验收标准文件代替discuss-phase。自动将需求解析到CONTEXT.md。完全跳过discuss-phase。
- `--ingest <path-or-glob>` — 使用一个或多个ADR文件代替discuss-phase。自动将锁定决策+范围围栏解析到CONTEXT.md。完全跳过discuss-phase。
- `--ingest-format <auto|nygard|madr|narrative>` — 可选ADR解析器格式覆盖（默认`auto`）
- `--reviews` — 结合来自REVIEWS.md的跨AI审查反馈重新规划（由`gsd-review skill`生成）
- `--text` — 使用纯文本编号列表代替TUI菜单（`/rc`远程会话必需）
- `--mvp` — 垂直MVP模式。规划器将任务组织为功能切片（UI→API→DB）而非水平层。在新项目的阶段1上，还会生成`SKELETON.md`（Walking Skeleton）。可通过ROADMAP.md中的`**Mode:** mvp`在阶段上持久化。

在第2步中，在任何目录查找之前规范化阶段输入。

## 指令

端到端执行。
保留所有工作流门控（验证、研究、规划、验证循环、路由）。

## 执行上下文

- `.trae/gsd/workflows/plan-phase.md`
- `.trae/gsd/references/ui-brand.md`

## 参数

- `[phase]`：阶段编号（可选——自动检测下一个未规划阶段）
- `--auto`：自动模式
- `--research`：强制重新研究
- `--skip-research`：跳过研究
- `--research-phase <N>`：仅研究模式
- `--view`：仅查看已有RESEARCH.md
- `--gaps`：差距闭合模式
- `--skip-verify`：跳过验证循环
- `--prd <file>`：使用PRD文件
- `--ingest <path-or-glob>`：使用ADR文件
- `--ingest-format <auto|nygard|madr|narrative>`：ADR解析格式
- `--reviews`：结合审查反馈重新规划
- `--text`：纯文本模式
- `--tdd`：TDD模式
- `--mvp`：垂直MVP模式

## 使用场景

- 需要为阶段创建详细的执行计划PLAN.md
- 需要在规划前进行领域研究
- 需要使用PRD或ADR文件代替discuss-phase
- 需要以MVP模式规划阶段

注意：本skill是GSD核心流程的一部分，在SOLO Coder中建议配合自定义智能体使用。GSD的讨论→规划→执行→验证循环与SOLO Coder的Plan模式互补。

## 不适用场景

- 阶段尚未在ROADMAP.md中创建
- 仅需查看阶段状态（应读取STATE.md）
- 需要执行阶段（应使用gsd-execute-phase）

## 输出

- `.trae/gsd/planning/phases/<phase>/PLAN.md`
- `.trae/gsd/planning/phases/<phase>/CONTEXT.md`
- `.trae/gsd/planning/phases/<phase>/RESEARCH.md`（如研究未跳过）
- `.trae/gsd/planning/phases/<phase>/SKELETON.md`（MVP模式阶段1）

## 依赖

- gsd-discuss-phase（默认流程中的讨论阶段）
- gsd-plan-checker（验证计划）
- gsd-phase-researcher（研究领域）
