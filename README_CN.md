# TRAE Skills — 来自 Claude Code 插件的技能移植

[English Documentation](./README.md)

TRAE_CN 是一款免费的 vibe coding 应用，其提供强大的模型供用户免费使用，且支持使用 Rules、Skills。但是 TRAE_CN 本身不为用户提供通用、强大的 skills 以充分发挥模型能力并进一步降低用户使用门槛，因此，我从 Claude Code 的知名插件（superpowers、oh-my-claudecode、get-shit-done、gstack）所提供的 skill 中选择了我认为好用的那一些，针对 TRAE_CN SOLO 做了适配改造，此外还自行组装了一套 AI Pipeline 技能集，大家可以下载后自行导入使用。

---

## 目录结构

```
├── ai-pipeline（一个使用Ralph保持运行的持续开发循环）/
├── frontend（前端及幻灯片）/
├── GSD技能移植/
├── gstack技能移植/
├── oh-my-claudecode技能移植/
└── superpowers技能移植/
```

---

## ai-pipeline（一个使用Ralph保持运行的持续开发循环）

自行组装的自动化工程流水线，提供从想法到生产级代码的完整流程。流水线以目标驱动循环运行，直到验收标准达标才停止。

| 技能名称 | 功能简介 |
|---------|---------|
| **ai-pipeline** | 完整 AI 工程流水线编排器：蓝图 → 架构决策记录 → 评估基准 → 自我改进 → 代码清理，循环运行直到目标达成 |
| **ai-slop-cleaner** | AI 生成代码清理器：以回归安全的方式删除死代码、合并重复逻辑、降低复杂度，不改变行为 |
| **architecture-decision-records** | 架构决策记录（ADR）：将编码过程中的架构决策自动捕获为结构化文档，记录上下文、备选方案和决策理由 |
| **blueprint** | 蓝图生成器：将一句话目标转化为分步施工计划，每步包含独立上下文摘要，支持依赖图和并行步骤检测 |
| **eval-harness** | 评估框架：实现评估驱动开发（EDD），定义通过/失败标准、pass@k 可靠性指标和回归测试套件 |
| **external-research** | 外部研究：当优化陷入瓶颈时，搜索 GitHub、arXiv、技术博客等外部资源，注入可操作的改进思路 |
| **self-improve** | 自我改进引擎：锦标赛式自动进化——多个改进方案并行竞争，胜者合并，持续优化直到基准分数达标 |

## frontend（前端及幻灯片）

前端开发相关技能，涵盖设计、模式和演示文稿制作。

| 技能名称 | 功能简介 |
|---------|---------|
| **frontend-design** | 前端设计：创建有辨识度、生产级的前端界面，强调视觉方向和设计意图，而非通用 AI 风格 UI |
| **frontend-patterns** | 前端开发模式：React/Next.js 组件模式、状态管理、性能优化、表单处理、动画和可访问性最佳实践 |
| **frontend-slides** | 前端幻灯片：创建零依赖、动画丰富的 HTML 演示文稿，支持 PPT 转换、视觉风格探索和视口自适应 |

## oh-my-claudecode 技能移植

源自 oh-my-claudecode 插件，提供从需求分析到代码交付的全流程技能。

| 技能名称 | 功能简介 |
|---------|---------|
| **autopilot** | 全自动驾驶：从简短产品想法到可运行代码的全自主执行——需求分析、技术设计、规划、并行实现、QA 循环、多视角验证 |
| **autoresearch** | 自动研究：有状态的单任务改进循环，配合严格评估器契约、Markdown 决策日志和最大运行时间限制 |
| **debug** | 调试诊断：使用日志、追踪和状态检查诊断会话或仓库问题，区分症状与根因 |
| **deep-dive** | 深度探究：2 阶段流水线——先追踪因果（3 条并行调查通道），再通过苏格拉底式访谈结晶需求 |
| **deep-interview** | 深度访谈：苏格拉底式深度提问 + 数学模糊度门控，在模糊度降至阈值前拒绝执行，确保需求清晰 |
| **deepinit** | 深度初始化：为整个代码库创建分层 AGENTS.md 文档，帮助 AI 代理理解目录结构、组件关系和工作约定 |
| **external-context** | 外部上下文：并行启动 2-5 个文档专家代理，搜索外部文档和参考资料 |
| **learner** | 学习器：从当前对话中提取可复用的学习技能，捕获非显而易见的变通方法和隐藏陷阱 |
| **omc-plan** | 战略规划：智能交互式规划，自动检测是否需要访谈，支持共识模式（Planner/Architect/Critic 循环） |
| **ralph** | Ralph 持久循环：PRD 驱动的持久执行循环，逐故事验证直到所有验收标准通过，含强制评审和代码清理 |
| **ralplan** | 共识规划入口：在执行前自动门控模糊的 ralph/autopilot/team 请求，确保计划经过充分论证 |
| **release** | 发布助手：分析仓库发布规则，缓存到配置文件，然后引导发布流程 |
| **remember** | 知识记忆：审查可复用的项目知识，决定哪些应保存到项目记忆、笔记本或持久文档中 |
| **sciomc** | 科学分析：编排并行科学家代理进行综合分析，支持 AUTO 模式 |
| **skillify** | 技能化：将当前会话中发现的可重复工作流转化为可复用的技能草稿 |
| **trace** | 追踪调查：证据驱动的追踪通道，编排竞争性追踪假设进行因果调查 |
| **ultraqa** | QA 循环：测试→验证→修复→重复的 QA 循环工作流，直到目标达成 |
| **ultrawork** | 并行执行：高吞吐量并行任务执行引擎，同时处理多个独立任务 |
| **verify** | 验证：在声称完成之前验证变更确实有效，提供功能、修复或重构的信心保障 |
| **visual-verdict** | 视觉判定：截图与参考图的结构化视觉 QA 比对，提供确定性的通过/失败判定 |
| **wiki** | 知识库：跨会话持续积累的 Markdown 知识库（Karpathy 模型） |
| **writing-plans** | 编写计划：在动手写代码之前，根据规格或需求编写多步骤实施计划 |
| **writing-skills** | 编写技能：创建新技能、编辑现有技能或验证技能在部署前是否正常工作 |

## superpowers 技能移植

源自 superpowers 插件，提供开发工作流和协作增强技能。

| 技能名称 | 功能简介 |
|---------|---------|
| **brainstorming** | 头脑风暴：在任何创造性工作之前必须使用——探索用户意图、需求和设计，再进入实现 |
| **dispatching-parallel-agents** | 并行代理调度：面对 2+ 个无共享状态或顺序依赖的独立任务时，并行派发代理执行 |
| **executing-plans** | 执行计划：在有书面实施计划时，在独立会话中执行并设置审查检查点 |
| **finishing-a-development-branch** | 完成开发分支：实现完成、测试通过后，引导选择合并、PR 或清理的集成方式 |
| **receiving-code-review** | 接收代码评审：收到代码评审反馈时使用，要求技术严谨和验证，而非盲目实施建议 |
| **requesting-code-review** | 请求代码评审：完成任务、实现功能或合并前，验证工作是否满足需求 |
| **self-improving-agent** | 自改进代理：从所有技能经验中学习的通用自改进代理，使用多记忆架构（语义+情景+工作）持续进化 |
| **skill-creator** | 技能创建器：创建新技能的必备工具 |
| **subagent-driven-development** | 子代理驱动开发：在当前会话中使用独立任务执行实施计划 |
| **systematic-debugging** | 系统化调试：遇到 bug、测试失败或意外行为时，在提出修复之前进行系统化调查 |
| **test-driven-development** | 测试驱动开发：实现任何功能或修复之前，先编写测试再写实现代码 |
| **using-git-worktrees** | 使用 Git Worktree：启动需要与当前工作区隔离的功能开发时，创建隔离的 git worktree |
| **using-superpowers** | 使用超能力：任何对话开始时使用——建立如何发现和使用技能的方法论 |

## GSD (Get-Shit-Done) 技能移植

源自 [get-shit-done](https://github.com/gsd-build/get-shit-done) 插件，提供从项目初始化到交付的完整项目管理工作流。GSD 实现了结构化的 讨论 → 规划 → 执行 → 验证 → 发布 循环，与 SOLO Coder 的 Plan/Spec 模式互补。

### 核心流程

| 技能名称 | 功能简介 |
|---------|---------|
| **gsd-new-project** | 初始化新项目：深度上下文收集 → 提问 → 调研 → 需求 → 路线图 |
| **gsd-discuss-phase** | 在规划前通过自适应提问收集阶段上下文 |
| **gsd-plan-phase** | 创建详细的阶段计划（PLAN.md），含调研和验证循环 |
| **gsd-execute-phase** | 使用基于 wave 的并行化方式执行所有阶段计划 |
| **gsd-verify-work** | 通过对话式 UAT 测试验证已构建的功能 |
| **gsd-ship** | 验证通过后创建 PR、运行评审并准备合并 |

### 项目管理

| 技能名称 | 功能简介 |
|---------|---------|
| **gsd-autonomous** | 自主运行所有剩余里程碑阶段：逐阶段执行讨论→规划→执行 |
| **gsd-manager** | 统一项目管理：状态查看、路由分发和跨 GSD 操作协调 |
| **gsd-new-milestone** | 为现有项目添加新里程碑 |
| **gsd-complete-milestone** | 完成并归档里程碑，含审计 |
| **gsd-milestone-summary** | 生成里程碑总结报告 |
| **gsd-progress** | 显示当前项目进度和状态 |
| **gsd-health** | 诊断项目健康状况，检测异常 |
| **gsd-stats** | 显示项目统计：阶段数、计划数、需求数、Git 指标 |

### 代码质量

| 技能名称 | 功能简介 |
|---------|---------|
| **gsd-code-review** | 跨 AI 代码审查，提供结构化反馈 |
| **gsd-debug** | 使用科学方法进行系统化调试，含持久状态 |
| **gsd-forensics** | 对失败的 GSD 工作流执行进行事后调查 |
| **gsd-audit-milestone** | 审计里程碑完整性和质量 |
| **gsd-audit-uat** | 跨阶段审计所有待处理的 UAT 和验证项 |
| **gsd-audit-fix** | 修复审计中发现的问题 |

### 快速操作

| 技能名称 | 功能简介 |
|---------|---------|
| **gsd-fast** | 内联执行简单任务——无子代理、无规划开销 |
| **gsd-quick** | 快速执行中小型任务，最少规划 |
| **gsd-capture** | 捕获想法、任务、笔记到目标位置 |
| **gsd-help** | 显示完整的 GSD 命令参考 |

### 专项阶段

| 技能名称 | 功能简介 |
|---------|---------|
| **gsd-ui-phase** | UI 专项阶段：设计、原型、实现和评审用户界面 |
| **gsd-ai-integration-phase** | AI 集成阶段：规划和实现 AI/ML 功能 |
| **gsd-secure-phase** | 安全阶段：审计和加固应用安全 |
| **gsd-mvp-phase** | MVP 阶段：以垂直切片构建最小可行产品 |
| **gsd-spec-phase** | 规格阶段：创建详细的技术规格说明 |
| **gsd-validate-phase** | 验证阶段：自动化测试和验证 |

### 知识与配置

| 技能名称 | 功能简介 |
|---------|---------|
| **gsd-map-codebase** | 使用并行映射代理分析代码库，生成结构化文档 |
| **gsd-graphify** | 构建、查询和检查项目知识图谱 |
| **gsd-extract-learnings** | 从已完成阶段产物中提取决策、教训和模式 |
| **gsd-ingest-docs** | 将外部文档（PRD、ADR）导入 GSD 规划上下文 |
| **gsd-config** | 配置 GSD 设置：工作流开关、高级参数、集成 |
| **gsd-settings** | 交互式 GSD 设置配置 |

### 工作流控制

| 技能名称 | 功能简介 |
|---------|---------|
| **gsd-pause-work** | 暂停当前工作会话，保留状态 |
| **gsd-resume-work** | 恢复暂停的工作会话 |
| **gsd-undo** | 安全回滚 GSD 阶段或计划提交，含依赖检查 |
| **gsd-pr-branch** | 为 GSD 阶段创建和管理 PR 分支 |
| **gsd-cleanup** | 清理已完成的 GSD 产物和临时文件 |
| **gsd-update** | 更新 GSD 到最新版本 |

### 其他工具

| 技能名称 | 功能简介 |
|---------|---------|
| **gsd-explore** | 探索项目结构，理解代码库 |
| **gsd-sketch** | 用一次性 HTML 原型探索 UI/设计想法 |
| **gsd-spike** | 时间盒技术调研，降低风险 |
| **gsd-review** | 跨 AI 评审项目交付物 |
| **gsd-review-backlog** | 审查和优先排序项目待办 |
| **gsd-add-tests** | 为项目添加测试 |
| **gsd-docs-update** | 更新项目文档 |
| **gsd-eval-review** | 评估和审查项目质量 |
| **gsd-plan-review-convergence** | 从多个 AI 视角收敛计划评审 |
| **gsd-ultraplan-phase** | 超详细规划，最大化上下文 |
| **gsd-thread** | 跨 GSD 会话管理对话线程 |
| **gsd-workspace** | 工作区管理和环境设置 |
| **gsd-workstreams** | 管理项目内的并行工作流 |
| **gsd-inbox** | 管理传入的任务和请求 |
| **gsd-import** | 将外部项目数据导入 GSD |
| **gsd-profile-user** | 配置用户档案和偏好 |
| **gsd-phase** | 通用阶段操作 |
| **gsd-ns-context** | 命名空间上下文管理 |
| **gsd-ns-ideate** | 命名空间构思和头脑风暴 |
| **gsd-ns-manage** | 命名空间管理操作 |
| **gsd-ns-project** | 命名空间项目操作 |
| **gsd-ns-review** | 命名空间审查操作 |
| **gsd-ns-workflow** | 命名空间工作流操作 |

## gstack 技能移植

源自 [gstack](https://github.com/garrytan/gstack) 插件（Garry Tan 出品），提供从规划到部署的完整工程工作流。gstack 实现了结构化的发布循环，包含金丝雀监控、多视角计划审查和设计咨询——专为快速且自信地交付的团队打造。

### 核心流程

| 技能名称 | 功能简介 |
|---------|---------|
| **gstack** | 根路由技能：会话初始化、技能路由、完成状态协议和自我改进 |
| **browse** | 网页浏览：搜索和获取网页内容，用于调研和上下文收集 |
| **ship** | 发布工作流：16 步发布流程，从分支创建到部署验证 |
| **investigate** | 系统化调试：5 阶段调查工作流，铁律"无根因不修复" |
| **qa** | QA 测试：10 阶段质量保证工作流，含健康评分规则 |
| **qa-only** | 仅 QA 模式：运行质量检查，不执行完整发布流程 |
| **canary** | 金丝雀监控：部署后金丝雀监控，含自动回滚触发 |
| **careful** | 谨慎模式：高风险变更的增强审查和验证 |
| **review** | 预落地 PR 审查：Review Army 专家调度，多视角代码审查 |
| **land-and-deploy** | 合并部署：合并验证和部署确认 |
| **health** | 健康仪表盘：6 维度代码质量评估 |

### 规划与审查

| 技能名称 | 功能简介 |
|---------|---------|
| **autoplan** | 自动规划：生成结构化计划，含依赖分析和并行步骤检测 |
| **plan-ceo-review** | CEO/创始人模式计划审查：4 种审查模式（创始人/VC/运营者/全部） |
| **plan-eng-review** | 工程计划审查：技术可行性、架构和实现评估 |
| **plan-design-review** | 设计计划审查：UX、视觉层次和交互质量评估 |
| **plan-devex-review** | 开发者体验审查：DX 实时审计，评估工具和工作流质量 |
| **plan-tune** | 计划调优：基于审查反馈的迭代计划优化 |

### 设计

| 技能名称 | 功能简介 |
|---------|---------|
| **design-consultation** | 设计咨询：专家设计反馈和建议 |
| **design-html** | HTML 设计：Pretext 文本布局引擎，生产级 HTML 生成 |
| **design-review** | 设计审查：视觉和交互质量评估 |
| **design-shotgun** | 设计散弹枪：快速多方案设计探索 |

### 办公与回顾

| 技能名称 | 功能简介 |
|---------|---------|
| **office-hours** | 办公时间：结构化问答和决策会议 |
| **retro** | 周度工程回顾，含全局回顾和比较模式 |
| **devex-review** | DX 审查：实时开发者体验审计 |

### 安全与文档

| 技能名称 | 功能简介 |
|---------|---------|
| **cso** | 首席安全官：全面安全审查和合规检查 |
| **document-generate** | 文档生成：Diataxis 框架文档创建 |
| **document-release** | 文档发布：发布后文档更新 |
| **learn** | 项目学习：捕获和管理项目知识 |
| **scrape** | 网页抓取：从网页提取数据 |

### 上下文与安全

| 技能名称 | 功能简介 |
|---------|---------|
| **context-save** | 上下文保存：保存会话上下文以供后续恢复 |
| **context-restore** | 上下文恢复：从保存的会话上下文恢复 |
| **freeze** | 冻结：限制编辑范围，防止意外修改 |
| **unfreeze** | 解冻：解除编辑限制 |
| **guard** | 守卫模式：完整安全模式，含全面保护规则 |

### 性能基准

| 技能名称 | 功能简介 |
|---------|---------|
| **benchmark** | 基准测试：Web 性能回归检测 |
| **benchmark-models** | 模型基准：模型性能比较和评估 |

### 配置与工具

| 技能名称 | 功能简介 |
|---------|---------|
| **gstack-codex** | OpenAI Codex CLI 封装器，替代模型访问 |
| **gstack-gstack-upgrade** | gstack 升级：更新到最新 gstack 版本 |
| **gstack-hackernews-frontpage** | Hacker News 首页：抓取和分析 HN 文章 |
| **gstack-landing-report** | 落地报告：版本队列状态和发布追踪 |
| **gstack-make-pdf** | 生成 PDF：Markdown 转 PDF |
| **gstack-open-gstack-browser** | 打开 gstack 浏览器：启动浏览器进行网页交互 |
| **gstack-pair-agent** | 配对代理：远程代理配对协作 |
| **gstack-setup-browser-cookies** | 配置浏览器 Cookie：设置浏览器认证 |
| **gstack-setup-deploy** | 配置部署：设置部署参数 |
| **gstack-setup-gbrain** | 配置 gbrain：设置知识库集成 |
| **gstack-skillify** | 技能化：浏览器技能编码和创建 |
| **gstack-sync-gbrain** | 同步 gbrain：同步知识库数据 |

### OpenClaw

| 技能名称 | 功能简介 |
|---------|---------|
| **gstack-openclaw-ceo-review** | OpenClaw CEO 审查：创始人视角计划审查 |
| **gstack-openclaw-investigate** | OpenClaw 调查：系统化问题调查 |
| **gstack-openclaw-office-hours** | OpenClaw 办公时间：结构化问答 |
| **gstack-openclaw-retro** | OpenClaw 回顾：工程回顾 |

---

## 使用方法

1. 下载对应技能的 `.zip` 文件
2. 在 TRAE_CN SOLO 中打开技能管理
3. 点击上传技能，选择下载的 zip 文件
4. 技能将自动解析并安装

> **注意**：每个 zip 文件均包含根级 `SKILL.md` 文件，符合 TRAE 官方技能格式规范。

## 致谢

- [superpowers](https://github.com/obra/superpowers) — Claude Code 插件
- [oh-my-claudecode](https://github.com/Yeachan-Heo/oh-my-claudecode) — Claude Code 插件
- [get-shit-done](https://github.com/gsd-build/get-shit-done) — Claude Code 插件
- [gstack](https://github.com/garrytan/gstack) — Claude Code 插件（Garry Tan 出品）

## 更新日志

### v4.0 — gstack 技能移植（52 个新技能）

- 新增来自 [gstack](https://github.com/garrytan/gstack) 插件（Garry Tan 出品）的 52 个技能
- 完整工程工作流：规划 → 审查 → 发布 → 金丝雀监控 → 回顾
- 路径适配：`~/.gstack/` → `.trae/gstack/data/`，`~/.claude/skills/` → `.trae/`
- 工具适配：CLI 工具引用（gstack CLI、浏览器工具、Codex CLI）添加 TRAE 替代方案说明
- Preamble 脚本 → 文字指令（TRAE 中无法运行 bash preamble 脚本）
- Hooks（PreToolUse）→ 指令中的检查步骤
- AskUserQuestion 格式 → 直接向用户提问
- 共享段落精简：每个技能约 700 行共享前导段落精简，只保留核心逻辑
- `$B`/`$D` 变量引用替换为文字说明
- `CLAUDE.md` 引用 → `.trae/rules/`
- YAML frontmatter 格式统一：52 个技能全部使用标准格式
- 52 个 zip 包全部通过格式合规性验证

### v3.0 — GSD 技能移植（66 个新技能）

- 新增来自 [get-shit-done](https://github.com/gsd-build/get-shit-done) (GSD) 插件的 66 个技能
- 完整的项目管理工作流：讨论 → 规划 → 执行 → 验证 → 发布
- 路径适配：`.planning/` → `.trae/gsd/planning/`
- 工具适配：`gsd-sdk`/`gsd-tools` CLI 引用添加 TRAE 替代方案说明
- 语言统一：所有描述和核心指令中文化
- SOLO 模式适配：每个技能添加与 SOLO Coder Plan/Spec 模式的关系说明
- 66 个 zip 包全部通过格式合规性验证

### v2.0 — SOLO 模式深度适配

- 路径适配：将 `.omc/`、`.claude/` 等旧路径统一替换为 `.trae/`
- 工具适配：将 Claude Code 特有工具引用替换为 TRAE SOLO 兼容替代方案
- 语言统一：所有技能描述和核心指令中文化
- SOLO 模式适配：每个技能添加与 SOLO Coder Plan/Spec 模式的关系说明
- 规范增强：添加"不适用场景"、"输出规范"、"依赖说明"段落
- 功能无损：所有核心指令、数据结构、参数阈值、示例代码完整保留

## License

MIT