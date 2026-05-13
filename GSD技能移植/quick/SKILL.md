---
name: gsd-quick
description: 当需要执行带有GSD保障（原子提交、状态跟踪）的快速任务但跳过可选代理时使用
---

# gsd-quick

## 描述

执行小型、临时任务，带有GSD保障（原子提交、STATE.md跟踪）。

快速模式是相同系统但路径更短：
- 生成gsd-planner（快速模式）+ gsd-executor(s)
- 快速任务存放在`.trae/gsd/planning/quick/`，与计划阶段分开
- 更新STATE.md的"Quick Tasks Completed"表（而非ROADMAP.md）

**默认**：跳过研究、讨论、计划检查器、验证器。当你确切知道要做什么时使用。

**`--discuss`标志**：规划前进行轻量级讨论阶段。揭示假设、澄清灰色地带、在CONTEXT.md中记录决策。当任务有值得预先解决的歧义时使用。

**`--full`标志**：启用完整质量管道——讨论 + 研究 + 计划检查 + 验证。一个标志搞定一切。

**`--validate`标志**：仅启用计划检查（最多2次迭代）和执行后验证。当你需要质量保障但不需要讨论或研究时使用。

**`--research`标志**：在规划前生成专注的研究代理。调查实现方法、库选项和任务陷阱。当你不确定最佳方案时使用。

细粒度标志可组合：`--discuss --research --validate`与`--full`效果相同。

**子命令：**
- `list` — 列出所有快速任务及其状态
- `status <slug>` — 显示特定快速任务的状态
- `resume <slug>` — 通过slug恢复特定快速任务

## 上下文

用户输入参数：`[list | status <slug> | resume <slug> | --full] [--validate] [--discuss] [--research] [任务描述]`

上下文文件在工作流内部解析（`init quick`）并通过`<files_to_read>`块委托。

## 指令

> **TRAE适配说明**：原文中引用的 `gsd-sdk` CLI工具在TRAE环境中不可用。在TRAE SOLO模式中，请直接读取 `.trae/gsd/planning/config.json` 和相关规划文件来获取配置信息，或使用TRAE的文件读取工具替代CLI查询。

**首先解析用户输入参数中的子命令：**

- 如果用户输入参数以"list"开头：SUBCMD=list
- 如果用户输入参数以"status "开头：SUBCMD=status，SLUG=剩余部分（去除空白，清理）
- 如果用户输入参数以"resume "开头：SUBCMD=resume，SLUG=剩余部分（去除空白，清理）
- 否则：SUBCMD=run，将完整用户输入参数原样传递给quick工作流

**Slug清理（用于status和resume）：** 去除不匹配`[a-z0-9-]`的字符。拒绝超过60个字符或包含`..`或`/`的slug。如果无效，输出"Invalid session slug."并停止。

### LIST子命令

当SUBCMD=list时：

```bash
ls -d .trae/gsd/planning/quick/*/  2>/dev/null
```

对于找到的每个目录：
- 检查PLAN.md是否存在
- 检查SUMMARY.md是否存在；如果存在，通过以下方式读取其frontmatter中的`status`：
  ```bash
  gsd-sdk query frontmatter.get .trae/gsd/planning/quick/{dir}/SUMMARY.md status
  ```
- 确定目录创建日期：`stat -f "%SB" -t "%Y-%m-%d"`（macOS）或`stat -c "%w"`（Linux）；回退到目录名中的日期前缀（格式：`YYYYMMDD-`前缀）
- 推导显示状态：
  - SUMMARY.md存在，frontmatter status=complete → `complete ✓`
  - SUMMARY.md存在，frontmatter status=incomplete或status缺失 → `incomplete`
  - SUMMARY.md缺失，目录创建 < 7天 → `in-progress`
  - SUMMARY.md缺失，目录创建 ≥ 7天 → `abandoned? (>7 days, no summary)`

**安全**：目录名从文件系统读取。在显示任何slug之前，进行清理：使用`name.replace(/[^\x20-\x7E]/g, '').replace(/[/\\]/g, '')`去除不可打印字符、ANSI转义序列和路径分隔符。永远不要通过字符串插值将原始目录名传递给shell命令。

显示格式：
```
Quick Tasks
────────────────────────────────────────────────────────────
slug                           date        status
backup-s3-policy               2026-04-10  in-progress
auth-token-refresh-fix         2026-04-09  complete ✓
update-node-deps               2026-04-08  abandoned? (>7 days, no summary)
────────────────────────────────────────────────────────────
3 tasks (1 complete, 2 incomplete/in-progress)
```

如果未找到目录：打印`No quick tasks found.`并停止。

显示列表后停止。不要继续后续步骤。

### STATUS子命令

当SUBCMD=status且SLUG已设置（已清理）时：

查找匹配`*-{SLUG}`模式的目录：
```bash
dir=$(ls -d .trae/gsd/planning/quick/*-{SLUG}/ 2>/dev/null | head -1)
```

如果未找到目录，打印`No quick task found with slug: {SLUG}`并停止。

读取给定slug的PLAN.md和SUMMARY.md（如果存在）。显示：
```
Quick Task: {slug}
─────────────────────────────────────
Plan file: .trae/gsd/planning/quick/{dir}/PLAN.md
Status: {status from SUMMARY.md frontmatter, or "no summary yet"}
Description: {first non-empty line from PLAN.md after frontmatter}
Last action: {last meaningful line of SUMMARY.md, or "none"}
─────────────────────────────────────
Resume with: gsd-quick resume {slug}
```

不生成代理。打印后停止。

### RESUME子命令

当SUBCMD=resume且SLUG已设置（已清理）时：

1. 查找匹配`*-{SLUG}`模式的目录：
   ```bash
   dir=$(ls -d .trae/gsd/planning/quick/*-{SLUG}/ 2>/dev/null | head -1)
   ```
2. 如果未找到目录，打印`No quick task found with slug: {SLUG}`并停止。

3. 读取PLAN.md提取描述，读取SUMMARY.md（如果存在）提取状态。

4. 在生成代理前打印：
   ```
   [quick] Resuming: .trae/gsd/planning/quick/{dir}/
   [quick] Plan: {description from PLAN.md}
   [quick] Status: {status from SUMMARY.md, or "in-progress"}
   ```

5. 通过以下方式加载上下文：
   ```bash
   gsd-sdk query init.quick
   ```

6. 继续执行带有恢复上下文的quick工作流，传递slug和计划目录，以便执行器从上次中断处继续。

### RUN子命令（默认）

当SUBCMD=run时：

端到端执行。
保留所有工作流门控（验证、任务描述、规划、执行、状态更新、提交）。

## 执行上下文

- `.trae/gsd/workflows/quick.md`

## 参数

- **--full**：启用完整质量管道——讨论 + 研究 + 计划检查 + 验证
- **--validate**：仅启用计划检查（最多2次迭代）和执行后验证
- **--discuss**：规划前进行轻量级讨论阶段
- **--research**：规划前生成专注的研究代理
- **--quick**：（在子命令中未使用，但某些工作流可能支持）

## 使用场景

- 需要快速完成一个小型任务，但希望保留GSD的原子提交和状态跟踪保障时
- 有明确的任务描述，不需要研究或讨论阶段时
- 需要管理多个快速任务的状态（列出、查看、恢复）时

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 大型功能开发需要完整规划流程时（应使用plan-phase + execute-phase）
- 需要跨多个阶段的复杂工作时（应使用标准GSD流程）

## 输出

- `.trae/gsd/planning/quick/YYYYMMDD-{slug}/` 目录，包含PLAN.md
- 完成后生成SUMMARY.md
- STATE.md中"Quick Tasks Completed"表更新

## 依赖

- gsd-plan-phase（快速模式规划）
- gsd-execute-phase（执行）
