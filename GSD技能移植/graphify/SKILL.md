---
name: gsd-graphify
description: 当需要构建、查询和检查.trae/gsd/planning/graphs/中的项目知识图谱时使用
---

# gsd-graphify

## 描述

构建、查询和检查 `.trae/gsd/planning/graphs/` 中的项目知识图谱。

## 指令

> **TRAE适配说明**：原文中引用的 `gsd-sdk` CLI工具在TRAE环境中不可用。在TRAE SOLO模式中，请直接读取 `.trae/gsd/planning/config.json` 和相关规划文件来获取配置信息，或使用TRAE的文件读取工具替代CLI查询。

### 步骤0 — 横幅

**在任何工具调用之前**，显示此横幅：

```
GSD > GRAPHIFY
```

然后继续步骤1。

### 步骤1 — 配置关卡

通过使用Read工具直接读取 `.trae/gsd/planning/config.json` 来检查graphify是否启用。

**不要使用gsd-tools config get-value命令** — 它在缺少键时会硬退出。

1. 使用Read工具读取 `.trae/gsd/planning/config.json`
2. 如果文件不存在：显示下方的禁用消息并 **停止**
3. 解析JSON内容。检查 `config.graphify && config.graphify.enabled === true`
4. 如果 `graphify.enabled` 未明确为 `true`：显示下方的禁用消息并 **停止**
5. 如果 `graphify.enabled` 为 `true`：继续步骤2

**禁用消息：**

```
GSD > GRAPHIFY

Knowledge graph is disabled. To activate:

  node gsd-tools config-set graphify.enabled true

Then run gsd-graphify skill build to create the initial graph.
```

---

### 步骤2 — 解析参数

解析用户输入参数以确定操作模式：

| 参数 | 动作 |
|------|------|
| `build` | 运行内联构建（步骤3） |
| `query <term>` | 运行内联查询（步骤2a） |
| `status` | 运行内联状态检查（步骤2b） |
| `diff` | 运行内联差异检查（步骤2c） |
| 无参数或未知 | 显示用法消息 |

**用法消息**（无参数或无法识别的参数时显示）：

```
GSD > GRAPHIFY

Usage: gsd-graphify skill <mode>

Modes:
  build           Build or rebuild the knowledge graph
  query <term>    Search the graph for a term
  status          Show graph freshness and statistics
  diff            Show changes since last build
```

#### 步骤2a — 查询

运行：

```bash
node gsd-tools graphify query <term>
```

解析JSON输出并显示结果：
- 如果输出包含 `"disabled": true`，显示步骤1的禁用消息并 **停止**
- 如果输出包含 `"error"` 字段，显示错误消息并 **停止**
- 如果未找到节点，显示：`No graph matches for '<term>'. Try gsd-graphify skill build to create or rebuild the graph.`
- 否则，按类型分组显示匹配节点，包含边关系和置信度层级（EXTRACTED/INFERRED/AMBIGUOUS）

显示结果后 **停止**。不要生成子代理。

#### 步骤2b — 状态

运行：

```bash
node gsd-tools graphify status
```

解析JSON输出并显示：
- 如果 `exists: false`，显示message字段
- 否则显示上次构建时间、节点/边/超边计数和STALE或FRESH指示器
- 如果 `built_at_commit` 非空，还显示 `Source commit:` 行：
  - `commit_stale === false`（在HEAD重建）：`Source commit: <built_at_commit> (current)`
  - `commit_stale === true`（图谱落后HEAD）：`Source commit: <built_at_commit> (<commits_behind> commits behind HEAD)`
  - `commit_stale === null`（不可达提交 / 无git）：`Source commit: <built_at_commit> (freshness unknown)`
- 如果 `built_at_commit` 为null（graphify v0.7之前的图谱），完全省略source-commit行 — 不要渲染"Source commit: unknown"

基于mtime的STALE/FRESH标志和基于commit的 `commit_stale` 衡量不同的事物，可能不一致（例如，CI构建的图谱在旧checkout上几分钟前重建，mtime上读为FRESH但 `commit_stale: true`）。
两者都展示以便代理选择。

显示状态后 **停止**。不要生成子代理。

#### 步骤2c — 差异

运行：

```bash
node gsd-tools graphify diff
```

解析JSON输出并显示：
- 如果 `no_baseline: true`，显示message字段
- 否则显示节点和边变更计数（added/removed/changed）

如果不存在快照，建议运行 `build` 两次（第一次创建，第二次生成差异基线）。

显示差异后 **停止**。不要生成子代理。

---

### 步骤3 — 构建（内联）

首先运行预检：

```bash
node "gsd-tools" graphify build
```

解析JSON输出：
- 如果 `disabled: true`：显示步骤1的禁用消息并 **停止**
- 如果 `error`：显示错误消息并 **停止**
- 如果 `action: "spawn_agent"`：预检通过 — 继续下面的内联构建

（`spawn_agent` 动作名称是历史遗留。skill现在内联执行构建，因为graphify v0.7+将构建拆分为快速AST提取阶段和单独的聚类+报告写入阶段。子代理隔离在代理退出时终止了后台bash，使缓存的提取阶段保持活跃但SIGTERM了提取后阶段，导致缓存已填充但未写入 `graph.json` 产物。CLI仍发出 `spawn_agent` 信号以保持外部调用者和测试正常工作。）

显示：

```text
GSD > Building knowledge graph...
```

在单个前台Bash调用中运行构建、复制产物、写入差异快照和报告摘要，使整个管道存活到完成。使用 `timeout` 为 `600000` 毫秒（10分钟），覆盖 `graphify.build_timeout` 上限（默认300秒）并留有余量：

```bash
graphify update . \
  && cp graphify-out/graph.json .trae/gsd/planning/graphs/graph.json \
  && cp graphify-out/graph.html .trae/gsd/planning/graphs/graph.html \
  && cp graphify-out/GRAPH_REPORT.md .trae/gsd/planning/graphs/GRAPH_REPORT.md \
  && node "gsd-tools" graphify build snapshot \
  && node "gsd-tools" graphify status
```

不要传递 `run_in_background: true`。典型构建在15-60秒内完成，整个链必须前台运行。

如果链失败（非零退出）：
- 显示：`## GRAPHIFY BUILD FAILED` 后跟捕获的stderr
- 不要删除 `.trae/gsd/planning/graphs/` — 之前的有效图谱仍可用
- **停止**

如果链成功：
- 解析尾随的 `graphify status` JSON
- 显示：`## GRAPHIFY BUILD COMPLETE`，包含节点、边和超边计数

---

### MVP模式节点渲染

**MVP模式渲染。** 当阶段在ROADMAP.md中有 `**Mode:** mvp`（通过 `gsd-sdk query roadmap.get-phase --pick mode` 解析）时，使用两个不同的视觉信号渲染其图谱节点：

1. **独特的填充颜色。** MVP模式阶段节点使用 `#22c55e`（绿色）。标准阶段保持默认填充颜色。双通道信号（颜色 + 标签）处理色盲和灰度渲染。
2. **`MVP` 标签后缀。** 在节点的标签文本后追加 ` (MVP)`。例如：原本标记为 `Phase 1: User Auth` 的阶段渲染为 `Phase 1: User Auth (MVP)`。

两个信号一起触发 — 永远不要只用一个。根据PRD Q5决策，目标是在任何渲染上下文中实现明确的视觉区分。

当阶段模式为null/缺失时，使用标准颜色和标签渲染 — 非MVP阶段无行为变更。

---

### 反模式

1. 不要为任何操作生成子代理 — build、query、status和diff都内联运行。子代理隔离在代理退出时终止后台bash，之前在写入中途截断graphify构建，只留下缓存已填充（#3166）。
2. 不要为构建链传递 `run_in_background: true` — 操作快速且必须在前台完成。
3. 不要直接修改图谱文件 — 始终通过 `graphify update .` 和快照CLI。
4. 不要跳过配置关卡检查。
5. 不要使用 `gsd-tools config get-value` 进行配置关卡 — 它在缺少键时退出。

## 执行上下文

- `.trae/gsd/workflows/graphify.md`（如有）

## 参数

- `build` — 构建或重建知识图谱
- `query <term>` — 搜索图谱中的术语
- `status` — 显示图谱新鲜度和统计
- `diff` — 显示自上次构建以来的变更

## 使用场景

- 需要可视化项目结构和依赖关系
- 需要查询项目知识图谱中的实体和关系
- 需要检查图谱是否与代码库同步

注意：本skill在SOLO Coder中作为GSD工作流的辅助工具使用。

## 不适用场景

- 项目规模过小无需知识图谱时
- graphify未在配置中启用时
- 不需要可视化项目结构时

## 输出

- `.trae/gsd/planning/graphs/graph.json` 知识图谱数据
- `.trae/gsd/planning/graphs/graph.html` 可视化页面
- `.trae/gsd/planning/graphs/GRAPH_REPORT.md` 图谱报告

## 依赖

- gsd-config（需先启用graphify配置）
