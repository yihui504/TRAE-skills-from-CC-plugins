---
name: gsd-complete-milestone
description: 当需要归档已完成的里程碑并准备下一版本时使用
---

# gsd-complete-milestone

## 描述

将里程碑 {{version}} 标记为完成，归档到milestones/，并更新ROADMAP.md和REQUIREMENTS.md。

目的：创建已发布版本的历史记录，归档里程碑产物（路线图 + 需求），并为下一里程碑做准备。
输出：里程碑已归档（路线图 + 需求），PROJECT.md已演进，git已打标签。

## 上下文

**项目文件：**
- `.trae/gsd/planning/ROADMAP.md`
- `.trae/gsd/planning/REQUIREMENTS.md`
- `.trae/gsd/planning/STATE.md`
- `.trae/gsd/planning/PROJECT.md`

**用户输入：**
- 版本：{{version}}（如"1.0"、"1.1"、"2.0"）

## 指令

**遵循complete-milestone.md工作流：**

0. **检查审计：**

   - 查找 `.trae/gsd/planning/v{{version}}-MILESTONE-AUDIT.md`
   - 如缺失或过时：建议先运行 `gsd-audit-milestone`
   - 如审计状态为 `gaps_found`：建议内联关闭差距
     （审计输出已列举差距 — 通过 `gsd-phase --insert <N>` 插入关闭阶段
     加上标准的 discuss/plan/execute 链）再继续。
   - 如审计状态为 `passed`：继续到步骤1

   ```markdown
   ## 预检

   {如无v{{version}}-MILESTONE-AUDIT.md:}
   ⚠ 未找到里程碑审计。请先运行 `gsd-audit-milestone` 以验证
   需求覆盖率、跨阶段集成和E2E流程。

   {如审计有差距:}
   ⚠ 里程碑审计发现差距。审计输出已列举未满足的需求、
   跨阶段问题和中断的流程 — 通过 `gsd-phase --insert <N>` 为每个差距
   插入关闭阶段，并运行标准的 `gsd-discuss-phase` → `gsd-plan-phase` → `gsd-execute-phase`
   链。或者继续以接受差距作为技术债务。

   {如审计通过:}
   ✓ 里程碑审计通过。继续完成。
   ```

1. **验证就绪状态：**

   - 检查里程碑中所有阶段是否有已完成的计划（SUMMARY.md存在）
   - 展示里程碑范围和统计
   - 等待确认

2. **收集统计：**

   - 统计阶段、计划、任务数量
   - 计算git范围、文件变更、LOC
   - 从git log提取时间线
   - 展示摘要，确认

3. **提取成就：**

   - 读取里程碑范围内所有阶段的SUMMARY.md文件
   - 提取4-6个关键成就
   - 展示以供批准

4. **归档里程碑：**

   - 创建 `.trae/gsd/planning/milestones/v{{version}}-ROADMAP.md`
   - 从ROADMAP.md提取完整阶段详情
   - 填充milestone-archive.md模板
   - 将ROADMAP.md更新为带链接的单行摘要

5. **归档需求：**

   - 创建 `.trae/gsd/planning/milestones/v{{version}}-REQUIREMENTS.md`
   - 将所有v1需求标记为完成（复选框勾选）
   - 注明需求结果（已验证、已调整、已放弃）
   - 删除 `.trae/gsd/planning/REQUIREMENTS.md`（下一里程碑会创建新的）

6. **更新PROJECT.md：**

   - 添加"当前状态"部分，包含已发布版本
   - 添加"下一里程碑目标"部分
   - 将之前内容归档在 `<details>` 中（如v1.1+）

7. **提交和打标签：**

   - 暂存：MILESTONES.md、PROJECT.md、ROADMAP.md、STATE.md、归档文件
   - 提交：`chore: archive v{{version}} milestone`
   - 标签：`git tag -a v{{version}} -m "[milestone summary]"`
   - 询问是否推送标签

8. **提供下一步操作：**
   - `gsd-new-milestone` — 开始下一里程碑（提问 → 研究 → 需求 → 路线图）

## 执行上下文

- `.trae/gsd/workflows/complete-milestone.md`
- `.trae/gsd/templates/milestone-archive.md`

## 参数

- `<version>` — 里程碑版本号（必需，如"1.0"、"1.1"）

## 使用场景

- 里程碑所有阶段完成并通过审计后需要归档
- 需要为已发布版本创建历史记录和git标签
- 需要准备进入下一里程碑

注意：本skill是GSD核心流程的一部分，在SOLO Coder中建议配合自定义智能体使用。GSD的讨论→规划→执行→验证循环与SOLO Coder的Plan模式互补。

## 不适用场景

- 里程碑尚有未完成阶段时
- 尚未运行里程碑审计时
- 需要继续在当前里程碑中工作时

## 输出

- 里程碑归档到 `.trae/gsd/planning/milestones/v{{version}}-ROADMAP.md`
- 需求归档到 `.trae/gsd/planning/milestones/v{{version}}-REQUIREMENTS.md`
- `.trae/gsd/planning/REQUIREMENTS.md` 已删除（为下一里程碑准备新的）
- ROADMAP.md折叠为单行条目
- PROJECT.md更新为当前状态
- Git标签v{{version}}已创建
- 提交成功

## 依赖

- gsd-audit-milestone（建议先完成审计）
- gsd-complete-milestone（依赖所有阶段完成）
