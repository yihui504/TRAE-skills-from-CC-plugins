# TRAE Skills — 来自 Claude Code 插件的技能移植

[English Documentation](./README.md)

TRAE_CN 是一款免费的 vibe coding 应用，其提供强大的模型供用户免费使用，且支持使用 Rules、Skills。但是 TRAE_CN 本身不为用户提供通用、强大的 skills 以充分发挥模型能力并进一步降低用户使用门槛，因此，我从 Claude Code 的知名插件（superpowers、oh-my-claudecode、get-shit-done）所提供的 skill 中选择了我认为好用的那一些，针对 TRAE_CN SOLO 做了适配改造，此外还自行组装了一套 AI Pipeline 技能集，大家可以下载后自行导入使用。

---

## 目录结构

```
├── ai-pipeline（一个使用Ralph保持运行的持续开发循环）/
├── frontend（前端及幻灯片）/
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

## License

MIT
