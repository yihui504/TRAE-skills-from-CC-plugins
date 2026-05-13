# TRAE Skills from Claude Code Plugins

[中文说明 / Chinese Documentation](./README_CN.md)

A collection of skills adapted for TRAE_CN SOLO, sourced from well-known Claude Code plugins (**superpowers**, **oh-my-claudecode**, **get-shit-done**) and custom-assembled pipelines.

TRAE_CN is a free vibe coding application that provides powerful models for free and supports Rules & Skills. However, TRAE_CN does not provide users with general, powerful skills to fully leverage model capabilities and lower the usage barrier. Therefore, I selected the most useful skills from well-known Claude Code plugins (superpowers, oh-my-claudecode, get-shit-done), adapted them for TRAE_CN SOLO, and also assembled a custom AI pipeline skill set. You can download and import them yourself.

---

## Directory Structure

```
├── ai-pipeline（一个使用Ralph保持运行的持续开发循环）/
├── frontend（前端及幻灯片）/
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

Frontend development skills covering design, patterns, and presentation creation.

| Skill | Description |
|-------|-------------|
| **frontend-design** | Frontend design: creates distinctive, production-grade interfaces with strong visual direction, avoiding generic AI-looking UI |
| **frontend-patterns** | Frontend patterns: React/Next.js component patterns, state management, performance optimization, form handling, animation, and accessibility best practices |
| **frontend-slides** | Frontend slides: creates zero-dependency, animation-rich HTML presentations with PPT conversion, visual style exploration, and viewport-safe layouts |

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

## License

MIT
