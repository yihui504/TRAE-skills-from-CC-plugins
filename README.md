# TRAE Skills from Claude Code Plugins

[中文说明 / Chinese Documentation](./README_CN.md)

A collection of skills adapted for TRAE_CN SOLO, sourced from well-known Claude Code plugins (**superpowers**, **oh-my-claudecode**, **get-shit-done**, **gstack**) and custom-assembled pipelines.

TRAE_CN is a free vibe coding application that provides powerful models for free and supports Rules & Skills. However, TRAE_CN does not provide users with general, powerful skills to fully leverage model capabilities and lower the usage barrier. Therefore, I selected the most useful skills from well-known Claude Code plugins (superpowers, oh-my-claudecode, get-shit-done, gstack), adapted them for TRAE_CN SOLO, and also assembled a custom AI pipeline skill set. You can download and import them yourself.

---

## Directory Structure

```
├── ai-pipeline（一个使用Ralph保持运行的持续开发循环）/
├── frontend（前端及幻灯片）/
├── GSD技能移植/
├── gstack技能移植/
├── oh-my-claudecode技能移植/
└── superpowers技能移植/
```

---

## ai-pipeline (A Continuous Development Loop Using Ralph)

A custom-assembled automated engineering pipeline from idea to production-grade code. The pipeline runs in a goal-driven loop until acceptance criteria are met.

| Skill | Description |
|-------|-------------|
| **ai-pipeline** | Full AI engineering pipeline orchestrator: blueprint → ADR → eval-harness → self-improve → slop-cleaner, loops until goal is met |
| **ai-slop-cleaner** | AI-generated code cleaner: regression-safe deletion-first workflow that removes dead code, merges duplicates, reduces complexity without changing behavior |
| **architecture-decision-records** | Architecture Decision Records (ADR): auto-captures architectural decisions as structured documents with context, alternatives, and rationale |
| **blueprint** | Blueprint generator: turns a one-line objective into a step-by-step construction plan with self-contained context briefs, dependency graphs, and parallel step detection |
| **eval-harness** | Evaluation framework: implements eval-driven development (EDD) with pass/fail criteria, pass@k reliability metrics, and regression test suites |
| **external-research** | External research: searches GitHub, arXiv, technical blogs and forums when optimization plateaus, injecting actionable improvement ideas |
| **self-improve** | Self-improvement engine: tournament-style auto-evolution with parallel plan competition, winner merging, continuous optimization until benchmark targets are met |

## frontend (Frontend & Slides)

Frontend development skills covering design, patterns, and presentation creation. **v4.1 Update: All three skills now include a mandatory "Phase 0: Style Discovery & Confirmation" workflow powered by [Refero Styles](https://styles.refero.design/). Before starting any implementation, the LLM will browse Refero's curated style library, extract design tokens (colors, typography, spacing, components), generate visual previews for user comparison, and only begin work after the user confirms their preferred style direction.**

| Skill | Description |
|-------|-------------|
| **frontend-design** | Frontend design: creates distinctive, production-grade interfaces with strong visual direction. **New: Mandatory Refero style discovery → preview generation → user selection → style lock before implementation** |
| **frontend-patterns** | Frontend patterns: React/Next.js component patterns, state management, performance optimization. **New: Visual style discovery when work involves UI rendering; Refero token-to-component mapping with role preservation rules** |
| **frontend-slides** | Frontend slides: creates zero-dependency HTML presentations. **New: Dual-source style discovery (Refero first + built-in presets fallback); mixed strategy supported** |

## oh-my-claudecode Skills Port

Sourced from the oh-my-claudecode plugin, providing full-lifecycle skills from requirements analysis to code delivery.

| Skill | Description |
|-------|-------------|
| **autopilot** | Full autonomous execution from idea to working code — requirements analysis, technical design, planning, parallel implementation, QA cycling, multi-perspective validation |
| **autoresearch** | Stateful single-mission improvement loop with strict evaluator contract, markdown decision logs, and max-runtime stop behavior |
| **debug** | Debug diagnostics: diagnoses session or repo state problems using logs, traces, and state inspection, distinguishing symptoms from root causes |
| **deep-dive** | Deep dive: 2-stage pipeline — trace (3 parallel causal investigation lanes) → deep-interview (requirements crystallization with 3-point injection) |
| **deep-interview** | Deep interview: Socratic questioning with mathematical ambiguity gating, refuses to proceed until ambiguity drops below threshold |
| **deepinit** | Deep initialization: creates hierarchical AGENTS.md documentation across the entire codebase for AI agent comprehension |
| **external-context** | External context: spawns 2-5 parallel document-specialist agents for external web searches and documentation lookup |
| **learner** | Learner: extracts reusable learned skills from the current conversation, capturing non-obvious workarounds and hidden gotchas |
| **omc-plan** | Strategic planning: intelligent interactive planning with auto-detection of interview needs, supports consensus mode (Planner/Architect/Critic loop) |
| **ralph** | Ralph persistence loop: PRD-driven persistent execution loop, story-by-story verification until all acceptance criteria pass, with mandatory review and code cleanup |
| **ralplan** | Consensus planning entrypoint: auto-gates vague ralph/autopilot/team requests before execution, ensuring plans are well-validated |
| **release** | Release assistant: analyzes repo release rules, caches them, then guides the release process |
| **remember** | Remember: reviews reusable project knowledge and decides what belongs in project memory, notepad, or durable docs |
| **sciomc** | Scientific analysis: orchestrates parallel scientist agents for comprehensive analysis with AUTO mode |
| **skillify** | Skillify: turns repeatable workflows from the current session into reusable skill drafts |
| **trace** | Trace: evidence-driven tracing lane that orchestrates competing tracer hypotheses for causal investigation |
| **ultraqa** | QA cycling: test → verify → fix → repeat workflow until goal is met |
| **ultrawork** | Parallel execution: high-throughput parallel task execution engine for simultaneous independent tasks |
| **verify** | Verify: verifies that a change really works before claiming completion, providing confidence in features, fixes, or refactors |
| **visual-verdict** | Visual verdict: structured visual QA for screenshot-to-reference comparisons with deterministic pass/fail guidance |
| **wiki** | Wiki: persistent markdown knowledge base that compounds across sessions (Karpathy model) |
| **writing-plans** | Writing plans: writes multi-step implementation plans from specs or requirements before touching code |
| **writing-skills** | Writing skills: creates new skills, edits existing skills, or verifies skills work before deployment |

## superpowers Skills Port

Sourced from the superpowers plugin, providing development workflow and collaboration enhancement skills.

| Skill | Description |
|-------|-------------|
| **brainstorming** | Brainstorming: MUST use before any creative work — explores user intent, requirements, and design before implementation |
| **dispatching-parallel-agents** | Dispatching parallel agents: dispatches agents in parallel when facing 2+ independent tasks without shared state or sequential dependencies |
| **executing-plans** | Executing plans: executes written implementation plans in a separate session with review checkpoints |
| **finishing-a-development-branch** | Finishing a development branch: guides completion of development work by presenting structured options for merge, PR, or cleanup |
| **receiving-code-review** | Receiving code review: requires technical rigor and verification when receiving code review feedback, not performative agreement or blind implementation |
| **requesting-code-review** | Requesting code review: verifies work meets requirements when completing tasks, implementing features, or before merging |
| **self-improving-agent** | Self-improving agent: universal self-improving agent that learns from ALL skill experiences using multi-memory architecture (semantic + episodic + working) |
| **skill-creator** | Skill creator: mandatory tool for creating new skills |
| **subagent-driven-development** | Subagent-driven development: executes implementation plans with independent tasks in the current session |
| **systematic-debugging** | Systematic debugging: systematic investigation before proposing fixes when encountering bugs, test failures, or unexpected behavior |
| **test-driven-development** | Test-driven development: writes tests before implementation code for any feature or bugfix |
| **using-git-worktrees** | Using git worktrees: creates isolated git worktrees for feature work that needs isolation from the current workspace |
| **using-superpowers** | Using superpowers: establishes how to find and use skills at the start of any conversation |

## GSD (Get-Shit-Done) Skills Port

Sourced from the [get-shit-done](https://github.com/gsd-build/get-shit-done) plugin, providing a complete project management workflow from initialization to delivery. GSD implements a structured discuss → plan → execute → verify → ship cycle that complements SOLO Coder's Plan/Spec modes.

### Core Workflow

| Skill | Description |
|-------|-------------|
| **gsd-new-project** | Initialize new project with deep context collection: questioning → research → requirements → roadmap |
| **gsd-discuss-phase** | Collect phase context through adaptive questioning before planning |
| **gsd-plan-phase** | Create detailed phase plans (PLAN.md) with research and verification loops |
| **gsd-execute-phase** | Execute all phase plans using wave-based parallelization |
| **gsd-verify-work** | Verify built features through conversational UAT testing |
| **gsd-ship** | Create PR, run reviews, and prepare for merge after verification passes |

### Project Management

| Skill | Description |
|-------|-------------|
| **gsd-autonomous** | Autonomously run all remaining milestone phases: discuss → plan → execute per phase |
| **gsd-manager** | Unified project manager: status, routing, and coordination across all GSD operations |
| **gsd-new-milestone** | Add a new milestone to an existing project |
| **gsd-complete-milestone** | Complete and archive a milestone with audit |
| **gsd-milestone-summary** | Generate milestone summary report |
| **gsd-progress** | Show current project progress and status |
| **gsd-health** | Diagnose project health and detect anomalies |
| **gsd-stats** | Display project statistics: phases, plans, requirements, git metrics |

### Code Quality

| Skill | Description |
|-------|-------------|
| **gsd-code-review** | Cross-AI code review with structured feedback |
| **gsd-debug** | Systematic debugging using scientific method with persistent state |
| **gsd-forensics** | Post-mortem investigation of failed GSD workflow executions |
| **gsd-audit-milestone** | Audit milestone completeness and quality |
| **gsd-audit-uat** | Cross-phase audit of all pending UAT and verification items |
| **gsd-audit-fix** | Fix issues found during audits |

### Quick Actions

| Skill | Description |
|-------|-------------|
| **gsd-fast** | Inline execution of simple tasks — no sub-agents, no planning overhead |
| **gsd-quick** | Quick execution with minimal planning for small-to-medium tasks |
| **gsd-capture** | Capture ideas, tasks, notes, and seeds to their target locations |
| **gsd-help** | Display complete GSD command reference |

### Specialized Phases

| Skill | Description |
|-------|-------------|
| **gsd-ui-phase** | UI-focused phase: design, prototype, implement, and review user interfaces |
| **gsd-ai-integration-phase** | AI integration phase: plan and implement AI/ML features |
| **gsd-secure-phase** | Security phase: audit and harden application security |
| **gsd-mvp-phase** | MVP phase: build minimum viable product with vertical slices |
| **gsd-spec-phase** | Specification phase: create detailed technical specifications |
| **gsd-validate-phase** | Validation phase: automated testing and validation |

### Knowledge & Configuration

| Skill | Description |
|-------|-------------|
| **gsd-map-codebase** | Analyze codebase with parallel mapping agents, generate structured documentation |
| **gsd-graphify** | Build, query, and inspect project knowledge graphs |
| **gsd-extract-learnings** | Extract decisions, lessons, patterns from completed phase artifacts |
| **gsd-ingest-docs** | Ingest external documents (PRD, ADR) into GSD planning context |
| **gsd-config** | Configure GSD settings: workflow toggles, advanced knobs, integrations |
| **gsd-settings** | Interactive GSD settings configuration |

### Workflow Control

| Skill | Description |
|-------|-------------|
| **gsd-pause-work** | Pause current work session with state preservation |
| **gsd-resume-work** | Resume a paused work session |
| **gsd-undo** | Safe git rollback of GSD phase or plan commits with dependency checking |
| **gsd-pr-branch** | Create and manage PR branches for GSD phases |
| **gsd-cleanup** | Clean up completed GSD artifacts and temporary files |
| **gsd-update** | Update GSD to the latest version |

### Additional Tools

| Skill | Description |
|-------|-------------|
| **gsd-explore** | Explore project structure and understand codebase |
| **gsd-sketch** | Explore UI/design ideas with disposable HTML prototypes |
| **gsd-spike** | Time-boxed technical investigation for risk reduction |
| **gsd-review** | Cross-AI review of project deliverables |
| **gsd-review-backlog** | Review and prioritize the project backlog |
| **gsd-add-tests** | Add tests to the project |
| **gsd-docs-update** | Update project documentation |
| **gsd-eval-review** | Evaluate and review project quality |
| **gsd-plan-review-convergence** | Converge plan reviews from multiple AI perspectives |
| **gsd-ultraplan-phase** | Ultra-detailed planning with maximum context |
| **gsd-thread** | Manage conversation threads across GSD sessions |
| **gsd-workspace** | Workspace management and environment setup |
| **gsd-workstreams** | Manage parallel workstreams within a project |
| **gsd-inbox** | Manage incoming tasks and requests |
| **gsd-import** | Import external project data into GSD |
| **gsd-profile-user** | Configure user profile and preferences |
| **gsd-phase** | Generic phase operations |
| **gsd-ns-context** | Namespace context management |
| **gsd-ns-ideate** | Namespace ideation and brainstorming |
| **gsd-ns-manage** | Namespace management operations |
| **gsd-ns-project** | Namespace project operations |
| **gsd-ns-review** | Namespace review operations |
| **gsd-ns-workflow** | Namespace workflow operations |

## gstack Skills Port

Sourced from the [gstack](https://github.com/garrytan/gstack) plugin by Garry Tan, providing a comprehensive engineering workflow from planning through deployment. gstack implements a structured ship cycle with canary monitoring, multi-perspective plan reviews, and design consultation — built for teams that ship fast with confidence.

### Core Workflow

| Skill | Description |
|-------|-------------|
| **gstack** | Root router skill: session initialization, skill routing, completion protocol, and self-improvement |
| **browse** | Web browsing: search and fetch web content for research and context gathering |
| **ship** | Ship workflow: 16-step release process from branch creation through deployment verification |
| **investigate** | Systematic debugging: 5-stage investigation workflow with "no root cause, no fix" principle |
| **qa** | QA testing: 10-stage quality assurance workflow with health scoring rules |
| **qa-only** | QA-only mode: run quality checks without full ship workflow |
| **canary** | Canary monitoring: post-deployment canary watch with automated rollback triggers |
| **careful** | Careful mode: enhanced review and validation for high-stakes changes |
| **review** | Pre-land PR review: Review Army expert dispatch for multi-perspective code review |
| **land-and-deploy** | Land and deploy: merge verification and deployment confirmation |
| **health** | Health dashboard: 6-dimension code quality assessment |

### Planning & Review

| Skill | Description |
|-------|-------------|
| **autoplan** | Auto-planning: generates structured plans with dependency analysis and parallel step detection |
| **plan-ceo-review** | CEO/Founder mode plan review: 4 review modes (Founder/VC/Operator/All) |
| **plan-eng-review** | Engineering plan review: technical feasibility, architecture, and implementation assessment |
| **plan-design-review** | Design plan review: UX, visual hierarchy, and interaction quality assessment |
| **plan-devex-review** | Developer experience review: DX real-time audit for tooling and workflow quality |
| **plan-tune** | Plan tuning: iterative plan refinement based on review feedback |

### Design

| Skill | Description |
|-------|-------------|
| **design-consultation** | Design consultation: expert design feedback and recommendations |
| **design-html** | HTML design: Pretext text layout engine for production-grade HTML generation |
| **design-review** | Design review: visual and interaction quality assessment |
| **design-shotgun** | Design shotgun: rapid multi-variant design exploration |

### Office & Retrospective

| Skill | Description |
|-------|-------------|
| **office-hours** | Office hours: structured Q&A and decision-making sessions |
| **retro** | Weekly engineering retrospective with global retro and comparison modes |
| **devex-review** | DX review: real-time developer experience audit |

### Security & Documentation

| Skill | Description |
|-------|-------------|
| **cso** | Chief Security Officer: comprehensive security review and compliance check |
| **document-generate** | Document generation: Diataxis framework documentation creation |
| **document-release** | Document release: post-ship documentation updates |
| **learn** | Project learning: capture and manage project knowledge |
| **scrape** | Web scraping: extract data from web pages |

### Context & Safety

| Skill | Description |
|-------|-------------|
| **context-save** | Context save: preserve session context for later restoration |
| **context-restore** | Context restore: resume from saved session context |
| **freeze** | Freeze: restrict editing scope to prevent unintended changes |
| **unfreeze** | Unfreeze: release editing restrictions |
| **guard** | Guard mode: full safety mode with comprehensive protection rules |

### Benchmarking

| Skill | Description |
|-------|-------------|
| **benchmark** | Benchmark: web performance regression detection |
| **benchmark-models** | Benchmark models: model performance comparison and evaluation |

### Setup & Utilities

| Skill | Description |
|-------|-------------|
| **gstack-codex** | OpenAI Codex CLI wrapper for alternative model access |
| **gstack-gstack-upgrade** | gstack upgrade: update to latest gstack version |
| **gstack-hackernews-frontpage** | Hacker News frontpage: fetch and analyze HN stories |
| **gstack-landing-report** | Landing report: version queue status and release tracking |
| **gstack-make-pdf** | Make PDF: convert Markdown to PDF |
| **gstack-open-gstack-browser** | Open gstack browser: launch browser for web interaction |
| **gstack-pair-agent** | Pair agent: remote agent pairing collaboration |
| **gstack-setup-browser-cookies** | Setup browser cookies: configure browser authentication |
| **gstack-setup-deploy** | Setup deploy: configure deployment parameters |
| **gstack-setup-gbrain** | Setup gbrain: configure knowledge base integration |
| **gstack-skillify** | Skillify: browser skill encoding and creation |
| **gstack-sync-gbrain** | Sync gbrain: synchronize knowledge base data |

### OpenClaw

| Skill | Description |
|-------|-------------|
| **gstack-openclaw-ceo-review** | OpenClaw CEO review: founder-perspective plan review |
| **gstack-openclaw-investigate** | OpenClaw investigate: systematic problem investigation |
| **gstack-openclaw-office-hours** | OpenClaw office hours: structured Q&A |
| **gstack-openclaw-retro** | OpenClaw retro: engineering retrospective |

---

## How to Use

1. Download the desired skill `.zip` file
2. Open Skill Management in TRAE_CN SOLO
3. Click Upload Skill and select the downloaded zip file
4. The skill will be automatically parsed and installed

> **Note**: Each zip file contains a root-level `SKILL.md` file, conforming to the official TRAE skill format specification.

## Credits

- [superpowers](https://github.com/obra/superpowers) — Claude Code plugin
- [oh-my-claudecode](https://github.com/Yeachan-Heo/oh-my-claudecode) — Claude Code plugin
- [get-shit-done](https://github.com/gsd-build/get-shit-done) — Claude Code plugin
- [gstack](https://github.com/garrytan/gstack) — Claude Code plugin (by Garry Tan)

## Changelog

### v4.1 — Frontend Skills: Refero Style Discovery Integration

- All three frontend skills now include a mandatory **Phase 0: Style Discovery & Confirmation** workflow
- Powered by [Refero Styles](https://styles.refero.design/) — curated design references extracted from real product pages
- Workflow: analyze requirements → browse Refero style library → extract design tokens → generate visual previews → user selects → style lock → begin implementation
- **frontend-design**: Full 6-step Phase 0 with UUID reference table, preview template, style lock format, Refero MCP optional enhancement, and fallback strategy
- **frontend-patterns**: Style discovery for visual work (skippable for logic-only tasks); new "Implementing Components with Refero Tokens" section with token mapping rules and role preservation
- **frontend-slides**: Dual-source style discovery (Refero first + built-in STYLE_PRESETS fallback); mixed strategy for combining Refero tokens with preset layouts/animations
- Style lock mechanism prevents implementation drift from user-confirmed direction
- Token role preservation rules: CTA colors stay CTA-only, border radii keep their specified elements, etc.

### v4.0 — gstack Skills Port (52 New Skills)

- Added 52 skills from the [gstack](https://github.com/garrytan/gstack) plugin (by Garry Tan)
- Complete engineering workflow: planning → review → ship → canary monitoring
- Multi-perspective plan reviews: CEO, engineering, design, and DX review modes
- Design consultation and multi-variant design exploration
- Security review (CSO), documentation generation, and context management
- All 52 zip packages verified through format compliance checks

### v3.0 — GSD Skills Port (66 New Skills)

- Added 66 skills from the [get-shit-done](https://github.com/gsd-build/get-shit-done) (GSD) plugin
- Complete project management workflow: discuss → plan → execute → verify → ship
- Path adaptation: `.planning/` → `.trae/gsd/planning/`
- Tool adaptation: `gsd-sdk`/`gsd-tools` CLI references annotated with TRAE alternatives
- Language unification: All descriptions and core instructions in Chinese
- SOLO mode adaptation: Each skill includes relationship notes with SOLO Coder Plan/Spec modes
- All 66 zip packages verified through format compliance checks

### v2.0 — Deep SOLO Mode Adaptation

- Path adaptation: Unified `.omc/`, `.claude/` paths to `.trae/`
- Tool adaptation: Replaced Claude Code-specific tool references with TRAE SOLO-compatible alternatives
- Language unification: All skill descriptions and core instructions in Chinese
- SOLO mode adaptation: Each skill includes relationship notes with SOLO Coder's Plan/Spec modes
- Spec compliance: Added "Not Applicable Scenarios", "Output Specification", and "Dependencies" sections
- Lossless functionality: All core instructions, data structures, parameter thresholds, and code examples are fully preserved

## License

MIT
