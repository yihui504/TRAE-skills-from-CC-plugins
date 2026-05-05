---
name: subagent-driven-development
description: Use when executing implementation plans with independent tasks in the current session
---

# 智能体驱动开发

Execute plan by 为每个任务调用独立智能体, with two-stage review after each: spec compliance review first, then code quality review.

**Why 智能体:** You delegate tasks to specialized agents with isolated context. By precisely crafting their instructions and context, you ensure they stay focused and succeed at their task. They should never inherit your session's context or history — you construct exactly what they need. This also preserves your own context for coordination work.

**Core principle:** 为每个任务调用独立智能体 + two-stage review (spec then quality) = high quality, fast iteration

## When to Use

```dot
digraph when_to_use {
    "Have implementation plan?" [shape=diamond];
    "Tasks mostly independent?" [shape=diamond];
    "Stay in this session?" [shape=diamond];
    "subagent-driven-development" [shape=box];
    "executing-plans" [shape=box];
    "Manual execution or brainstorm first" [shape=box];

    "Have implementation plan?" -> "Tasks mostly independent?" [label="yes"];
    "Have implementation plan?" -> "Manual execution or brainstorm first" [label="no"];
    "Tasks mostly independent?" -> "Stay in this session?" [label="yes"];
    "Tasks mostly independent?" -> "Manual execution or brainstorm first" [label="no - tightly coupled"];
    "Stay in this session?" -> "subagent-driven-development" [label="yes"];
    "Stay in this session?" -> "executing-plans" [label="no - parallel session"];
}
```

**vs. Executing Plans (parallel session):**
- Same session (no context switch)
- 为每个任务调用独立智能体 (no context pollution)
- Two-stage review after each task: spec compliance first, then code quality
- Faster iteration (no human-in-loop between tasks)

## The Process

```dot
digraph process {
    rankdir=TB;

    subgraph cluster_per_task {
        label="Per Task";
        "调用 @backend-architect 智能体（带实现指令）(./implementer-prompt.md)" [shape=box];
        "实现智能体 asks questions?" [shape=diamond];
        "Answer questions, provide context" [shape=box];
        "实现智能体 implements, tests, commits, self-reviews" [shape=box];
        "调用 @backend-architect 智能体（带规格审查指令）(./spec-reviewer-prompt.md)" [shape=box];
        "规格审查智能体 confirms code matches spec?" [shape=diamond];
        "实现智能体 fixes spec gaps" [shape=box];
        "调用 @backend-architect 智能体（带代码质量审查指令）(./code-quality-reviewer-prompt.md)" [shape=box];
        "代码质量审查智能体 approves?" [shape=diamond];
        "实现智能体 fixes quality issues" [shape=box];
        "Mark task complete in TodoWrite" [shape=box];
    }

    "Read plan, extract all tasks with full text, note context, create TodoWrite" [shape=box];
    "More tasks remain?" [shape=diamond];
    "调用 @backend-architect 智能体（带最终审查指令）for entire implementation" [shape=box];
    "Use superpowers:finishing-a-development-branch" [shape=box style=filled fillcolor=lightgreen];

    "Read plan, extract all tasks with full text, note context, create TodoWrite" -> "调用 @backend-architect 智能体（带实现指令）(./implementer-prompt.md)";
    "调用 @backend-architect 智能体（带实现指令）(./implementer-prompt.md)" -> "实现智能体 asks questions?";
    "实现智能体 asks questions?" -> "Answer questions, provide context" [label="yes"];
    "Answer questions, provide context" -> "调用 @backend-architect 智能体（带实现指令）(./implementer-prompt.md)";
    "实现智能体 asks questions?" -> "实现智能体 implements, tests, commits, self-reviews" [label="no"];
    "实现智能体 implements, tests, commits, self-reviews" -> "调用 @backend-architect 智能体（带规格审查指令）(./spec-reviewer-prompt.md)";
    "调用 @backend-architect 智能体（带规格审查指令）(./spec-reviewer-prompt.md)" -> "规格审查智能体 confirms code matches spec?";
    "规格审查智能体 confirms code matches spec?" -> "实现智能体 fixes spec gaps" [label="no"];
    "实现智能体 fixes spec gaps" -> "调用 @backend-architect 智能体（带规格审查指令）(./spec-reviewer-prompt.md)" [label="re-review"];
    "规格审查智能体 confirms code matches spec?" -> "调用 @backend-architect 智能体（带代码质量审查指令）(./code-quality-reviewer-prompt.md)" [label="yes"];
    "调用 @backend-architect 智能体（带代码质量审查指令）(./code-quality-reviewer-prompt.md)" -> "代码质量审查智能体 approves?";
    "代码质量审查智能体 approves?" -> "实现智能体 fixes quality issues" [label="no"];
    "实现智能体 fixes quality issues" -> "调用 @backend-architect 智能体（带代码质量审查指令）(./code-quality-reviewer-prompt.md)" [label="re-review"];
    "代码质量审查智能体 approves?" -> "Mark task complete in TodoWrite" [label="yes"];
    "Mark task complete in TodoWrite" -> "More tasks remain?";
    "More tasks remain?" -> "调用 @backend-architect 智能体（带实现指令）(./implementer-prompt.md)" [label="yes"];
    "More tasks remain?" -> "调用 @backend-architect 智能体（带最终审查指令）for entire implementation" [label="no"];
    "调用 @backend-architect 智能体（带最终审查指令）for entire implementation" -> "Use superpowers:finishing-a-development-branch";
}
```

## Model Selection

Use the least powerful model that can handle each role to conserve cost and increase speed.

**Mechanical implementation tasks** (isolated functions, clear specs, 1-2 files): use a fast, cheap model. Most implementation tasks are mechanical when the plan is well-specified.

**Integration and judgment tasks** (multi-file coordination, pattern matching, debugging): use a standard model.

**Architecture, design, and review tasks**: use the most capable available model.

**Task complexity signals:**
- Touches 1-2 files with a complete spec → cheap model
- Touches multiple files with integration concerns → standard model
- Requires design judgment or broad codebase understanding → most capable model

## Handling Implementer Status

Implementer 智能体 report one of four statuses. Handle each appropriately:

**DONE:** Proceed to spec compliance review.

**DONE_WITH_CONCERNS:** The implementer completed the work but flagged doubts. Read the concerns before proceeding. If the concerns are about correctness or scope, address them before review. If they're observations (e.g., "this file is getting large"), note them and proceed to review.

**NEEDS_CONTEXT:** The implementer needs information that wasn't provided. Provide the missing context and re-dispatch.

**BLOCKED:** The implementer cannot complete the task. Assess the blocker:
1. If it's a context problem, provide more context and re-dispatch with the same model
2. If the task requires more reasoning, re-dispatch with a more capable model
3. If the task is too large, break it into smaller pieces
4. If the plan itself is wrong, escalate to the human

**Never** ignore an escalation or force the same model to retry without changes. If the implementer said it's stuck, something needs to change.

## Prompt Templates

- `./implementer-prompt.md` - 调用 @backend-architect 智能体（带实现指令）
- `./spec-reviewer-prompt.md` - 调用 @backend-architect 智能体（带规格审查指令）
- `./code-quality-reviewer-prompt.md` - 调用 @backend-architect 智能体（带代码质量审查指令）

## Example Workflow

```
You: I'm using 智能体驱动开发 to execute this plan.

[Read plan file once: docs/superpowers/plans/feature-plan.md]
[Extract all 5 tasks with full text and context]
[Create TodoWrite with all tasks]

Task 1: Hook installation script

[Get Task 1 text and context (already extracted)]
[调用 @backend-architect 智能体（带实现指令）with full task text + context]

Implementer: "Before I begin - should the hook be installed at user or system level?"

You: "User level (~/.config/superpowers/hooks/)"

Implementer: "Got it. Implementing now..."
[Later] Implementer:
  - Implemented install-hook command
  - Added tests, 5/5 passing
  - Self-review: Found I missed --force flag, added it
  - Committed

[调用 @backend-architect 智能体（带规格审查指令）]
Spec reviewer: ✅ Spec compliant - all requirements met, nothing extra

[Get git SHAs, 调用 @backend-architect 智能体（带代码质量审查指令）]
Code reviewer: Strengths: Good test coverage, clean. Issues: None. Approved.

[Mark Task 1 complete]

Task 2: Recovery modes

[Get Task 2 text and context (already extracted)]
[调用 @backend-architect 智能体（带实现指令）with full task text + context]

Implementer: [No questions, proceeds]
Implementer:
  - Added verify/repair modes
  - 8/8 tests passing
  - Self-review: All good
  - Committed

[调用 @backend-architect 智能体（带规格审查指令）]
Spec reviewer: ❌ Issues:
  - Missing: Progress reporting (spec says "report every 100 items")
  - Extra: Added --json flag (not requested)

[Implementer fixes issues]
Implementer: Removed --json flag, added progress reporting

[Spec reviewer reviews again]
Spec reviewer: ✅ Spec compliant now

[调用 @backend-architect 智能体（带代码质量审查指令）]
Code reviewer: Strengths: Solid. Issues (Important): Magic number (100)

[Implementer fixes]
Implementer: Extracted PROGRESS_INTERVAL constant

[Code reviewer reviews again]
Code reviewer: ✅ Approved

[Mark Task 2 complete]

...

[After all tasks]
[调用 @backend-architect 智能体（带最终审查指令）]
Final reviewer: All requirements met, ready to merge

Done!
```

## Advantages

**vs. Manual execution:**
- 智能体 follow TDD naturally
- Fresh context per task (no confusion)
- Parallel-safe (智能体 don't interfere)
- 智能体 can ask questions (before AND during work)

**vs. Executing Plans:**
- Same session (no handoff)
- Continuous progress (no waiting)
- Review checkpoints automatic

**Efficiency gains:**
- No file reading overhead (controller provides full text)
- Controller curates exactly what context is needed
- 智能体 gets complete information upfront
- Questions surfaced before work begins (not after)

**Quality gates:**
- Self-review catches issues before handoff
- Two-stage review: spec compliance, then code quality
- Review loops ensure fixes actually work
- Spec compliance prevents over/under-building
- Code quality ensures implementation is well-built

**Cost:**
- More 智能体 invocations (implementer + 2 reviewers per task)
- Controller does more prep work (extracting all tasks upfront)
- Review loops add iterations
- But catches issues early (cheaper than debugging later)

## Red Flags

**Never:**
- Start implementation on main/master branch without explicit user consent
- Skip reviews (spec compliance OR code quality)
- Proceed with unfixed issues
- Dispatch multiple implementation 智能体 in parallel (conflicts)
- Make 智能体 read plan file (provide full text instead)
- Skip scene-setting context (智能体 needs to understand where task fits)
- Ignore 智能体 questions (answer before letting them proceed)
- Accept "close enough" on spec compliance (spec reviewer found issues = not done)
- Skip review loops (reviewer found issues = implementer fixes = review again)
- Let implementer self-review replace actual review (both are needed)
- **Start code quality review before spec compliance is ✅** (wrong order)
- Move to next task while either review has open issues

**If 智能体 asks questions:**
- Answer clearly and completely
- Provide additional context if needed
- Don't rush them into implementation

**If reviewer finds issues:**
- Implementer (same 智能体) fixes them
- Reviewer reviews again
- Repeat until approved
- Don't skip the re-review

**If 智能体 fails task:**
- 调用修复智能体 with specific instructions
- Don't try to fix manually (context pollution)

## Integration

**Required workflow skills:**
- **superpowers:using-git-worktrees** - REQUIRED: Set up isolated workspace before starting
- **superpowers:writing-plans** - Creates the plan this skill executes
- **superpowers:requesting-code-review** - Code review template for reviewer subagents
- **superpowers:finishing-a-development-branch** - Complete development after all tasks

**智能体 should use:**
- **superpowers:test-driven-development** - 智能体 follow TDD for each task

**Alternative workflow:**
- **superpowers:executing-plans** - Use for parallel session instead of same-session execution