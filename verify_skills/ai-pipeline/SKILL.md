---
name: ai-pipeline
description: "Orchestrate the full AI engineering pipeline from idea to production-grade code. Runs blueprint → architecture-decision-records → eval-harness → self-improve → ai-slop-cleaner in a loop until the acceptance criteria are met. TRIGGER when: user says \"run the pipeline\", \"ai-pipeline\", \"full pipeline\", describes a complex improvement goal that needs the complete workflow, or asks to go from idea to delivery. DO NOT TRIGGER when: task is simple enough for a single skill, or user explicitly invokes a specific pipeline phase."
---

# AI Pipeline — From Idea to Production-Grade Code

Orchestrate the complete AI engineering pipeline in a goal-driven loop. The pipeline does not simply run once and stop — it cycles until the acceptance criteria defined in eval-harness are met, re-planning and re-evolving as needed.

## When to Use

- User says "run the pipeline", "ai-pipeline", "full pipeline"
- User describes a complex improvement goal needing the complete workflow
- User wants to go from a vague idea to delivered, clean code
- User says anything that implies the full "think → record → measure → evolve → clean" cycle

**Do NOT use** when:
- The task is simple enough for a single skill
- User explicitly invokes a specific pipeline phase (e.g., "just run blueprint")
- User says "just do it" for a small task

## Pipeline Overview

The pipeline is a **goal-driven loop**, not a one-shot sequence:

```
[User Goal]
     │
     ▼
 ┌─────────────────────────────────────────────────────────────────┐
 │  Phase 1: blueprint                                              │
 │  Turn a one-line objective into a step-by-step construction plan │
 │  Output: Dependency graph + parallel steps + context briefs      │
 └──────────────────────────┬──────────────────────────────────────┘
                            │
                            ▼
 ┌─────────────────────────────────────────────────────────────────┐
 │  Phase 2: architecture-decision-records                          │
 │  Capture architectural decisions as structured ADRs              │
 │  Output: ADR documents (context, alternatives, rationale)        │
 └──────────────────────────┬──────────────────────────────────────┘
                            │
                            ▼
 ┌─────────────────────────────────────────────────────────────────┐
 │  Phase 3: eval-harness                                           │
 │  Define quantifiable evaluation criteria and benchmarks          │
 │  Output: Eval suite + baseline scores + acceptance criteria      │
 └──────────────────────────┬──────────────────────────────────────┘
                            │
                            ▼
 ┌─────────────────────────────────────────────────────────────────┐
 │  Phase 4: self-improve                                           │
 │  Tournament-style auto-evolution — parallel plans compete        │
 │  Output: Continuously improved code + progress chart + history   │
 └──────────────────────────┬──────────────────────────────────────┘
                            │
                            ▼
 ┌─────────────────────────────────────────────────────────────────┐
 │  Phase 5: ai-slop-cleaner                                        │
 │  Regression-safe code cleanup — delete dead code, merge dupes    │
 │  Output: Refined production-grade code                           │
 └──────────────────────────┬──────────────────────────────────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │  Acceptance Check    │
                 │  Goal met?           │
                 └──────┬──────┬───────┘
                        │      │
                   YES  │      │  NO
                        │      │
                        ▼      ▼
               [Deliver &    ┌──────────────────────────────────────┐
                Exit]        │  Bottleneck Check                     │
                             │  Score plateaued 5+ cycles?           │
                             └──────┬──────────────┬────────────────┘
                                    │              │
                               YES  │              │  NO
                                    │              │
                                    ▼              ▼
                        ┌──────────────────┐   Re-enter loop
                        │  Phase 6:         │   (Phase 4)
                        │  external-research│
                        │  (conditional)    │
                        └────────┬─────────┘
                                 │
                                 ▼
                          Re-enter loop
                          (Phase 4 or Phase 1)
```

### Loop Behavior

After each full pass (or after self-improve + slop-cleaner), evaluate whether the acceptance criteria are met:

- **Goal met** → Deliver results, exit pipeline
- **Goal not met, but making progress** → Re-enter at Phase 4 (self-improve) with updated strategy, new ideas fed via `idea.md`
- **Goal not met, and stuck (plateau or all approaches exhausted)** → Re-enter at Phase 1 (blueprint) to re-plan with a fundamentally different strategy, then continue through all phases
- **Goal not met, and acceptance criteria need adjustment** → Consult user: refine the goal, adjust target values, or expand scope

The loop continues **without any upper limit** until one of these exit conditions is met:
1. **Acceptance criteria met** — the benchmark score reaches the target
2. **User explicitly stops** the pipeline

### Bottleneck Detection & External Research (Phase 6)

When the pipeline detects a **bottleneck** — the score has not improved for the last 5 cycles — it triggers **Phase 6: external-research** as a conditional pipeline phase.

**Trigger condition**: `cycle_count >= 10` AND `score has not improved in the last 5 cycles` (compare current score against the best score from 5 cycles ago).

**What happens**: Invoke the `external-research` skill (技能: external-research), passing:
- The original objective and acceptance criteria
- Current score vs target score
- All approaches tried (from iteration history)
- ADR records
- Codebase summary
- Output path: `<self-improve-root>/config/idea.md`

The external-research skill will:
1. Search GitHub, arXiv, technical blogs, and forums for reference implementations and inspiration
2. Deeply analyze findings and map them to the current codebase
3. Write concrete, actionable ideas to `idea.md` — each with source, technique, estimated impact, and how it differs from prior attempts
4. **Never relax hard constraints**: original goal, acceptance criteria, evaluation benchmark, and regression thresholds remain absolute

**After external-research completes**, re-enter the loop:
- If new ideas are incremental → re-enter at Phase 4 (self-improve)
- If findings suggest a fundamentally different approach → re-enter at Phase 1 (blueprint)

**Re-trigger**: External research triggers again after another 10 cycles if the score plateaus for another 5 cycles.

## Instructions

### Step 0: Gather Goal (Deep Interactive Guidance)

Accept the user's goal in any form — from a one-liner to a detailed spec. **Thoroughly understand the goal before starting.** Ask as many clarifying questions as needed. Do not rush into execution with an unclear objective.

**Required information** (must obtain before starting):
1. **Objective**: What exactly should improve? Be specific. (e.g., not "make it better" but "reduce recommendation latency to under 100ms")
2. **Target repo**: Which repository? (default: current project directory)

**Strongly recommended information** (ask if not provided — these significantly affect pipeline effectiveness):
3. **Target metric and value**: How will you measure success? What number constitutes "done"? (e.g., "p99 latency < 100ms", "test coverage > 90%")
4. **Scope**: Which files/modules are in scope? Which are out of bounds?
5. **Constraints**: Any hard constraints? (e.g., "must not change the public API", "budget limited to $X in compute")

**Additional context to explore** (ask when relevant):
6. **Current baseline**: Do you know the current performance? Any existing benchmarks?
7. **Prior attempts**: Has this been tried before? What happened?
8. **Business context**: Why does this matter? What's the urgency?
9. **Acceptance criteria**: Beyond the primary metric, are there any other conditions for "done"? (e.g., "must also pass security audit")
10. **Risk tolerance**: How aggressive can the optimizations be? Is stability more important than peak performance?

**Guidance principles**:
- Ask ONE question at a time, prioritized by impact on pipeline effectiveness
- There is NO upper limit on questions — keep asking until the goal is crystal clear
- Use the target repo to inform your questions (read README, check existing tests, understand the codebase)
- When the user provides partial information, acknowledge it and ask the next most important question
- Only start the pipeline when you are confident you understand: WHAT to improve, HOW to measure it, and WHAT "done" looks like
- If the user explicitly says "start now" or "that's enough", proceed with what you have

### Step 1: Launch Phase 1 — Blueprint

Invoke the `blueprint` skill with the user's objective.

**What to do**:
1. Load the blueprint skill (技能: blueprint)
2. Execute the blueprint pipeline: Research → Design → Draft → Review → Register
3. The blueprint will produce a plan file in `plans/`

**Output checkpoint**: Plan file exists at `plans/{slug}.md`

**On failure**: If blueprint cannot produce a plan (e.g., objective too vague), go back to Step 0 and ask more clarifying questions. Do NOT proceed with a weak plan.

**On re-entry (loop)**: When re-entering from the loop because the strategy is stuck, explicitly tell blueprint that prior approaches failed and a fundamentally different decomposition is needed. Feed the gap analysis (current score vs target, what has been tried) as context.

### Step 2: Launch Phase 2 — Architecture Decision Records

Invoke the `architecture-decision-records` skill to capture decisions from the blueprint.

**What to do**:
1. Load the architecture-decision-records skill (技能: architecture-decision-records)
2. Review the blueprint plan for architectural choices
3. Create ADRs for each significant decision in the plan
4. Initialize `docs/adr/` if it doesn't exist

**Output checkpoint**: ADR files exist in `docs/adr/`

**On failure**: Log warning, continue. ADR capture is important but not blocking.

### Step 3: Launch Phase 3 — Eval Harness

Invoke the `eval-harness` skill to define success metrics and **acceptance criteria**.

**What to do**:
1. Load the eval-harness skill (技能: eval-harness)
2. Define capability evals based on the blueprint's exit criteria
3. Define regression evals for existing functionality
4. Create or identify a benchmark script
5. Validate the benchmark (3 runs, variance < 5%)
6. Record baseline scores
7. **Define acceptance criteria**: What benchmark score constitutes "goal met"? This becomes the pipeline's exit condition.

**Output checkpoint**:
- Eval definitions in `.trae/evals/`
- Benchmark script that outputs a score
- Baseline score recorded
- Acceptance criteria defined (target score + direction)

**On failure**: If benchmark cannot be created, ask user to provide a benchmark command. If user cannot provide one, report and exit — the pipeline requires a quantifiable acceptance criterion to function as a loop.

### Step 4: Launch Phase 4 — Self-Improve

Invoke the `self-improve` skill to run the evolution loop.

**What to do**:
1. Load the self-improve skill (技能: self-improve)
2. The self-improve skill will:
   - Set up its state directory using the benchmark from Phase 3
   - Run the improvement loop autonomously
   - Use the eval-harness benchmark as its evaluation criteria
   - Use ADRs from Phase 2 to avoid repeating failed approaches
   - Stop when a stop condition is met (target reached, plateau, max iterations, etc.)
3. Do NOT interrupt the self-improve loop — it runs autonomously

**Output checkpoint**:
- Improved code on `improve/{goal_slug}` branch
- Progress chart at `.trae/self-improve/topics/{slug}/tracking/progress.png`
- Iteration history recorded

**On failure**: If self-improve cannot start (e.g., no benchmark), report and skip to Phase 5 with current code.

**On re-entry (loop)**: When re-entering self-improve from the outer loop, feed new strategy ideas into `<self-improve-root>/config/idea.md`. Reset the circuit breaker count. If the prior self-improve run plateaued, consider adjusting `number_of_agents` or `target_value` in settings.

### Step 5: Launch Phase 5 — AI Slop Cleaner

Invoke the `ai-slop-cleaner` skill to clean up evolution residue.

**What to do**:
1. Load the ai-slop-cleaner skill (技能: ai-slop-cleaner)
2. Run the deletion-first cleanup workflow:
   - Pass 1: Dead code deletion
   - Pass 2: Duplicate removal
   - Pass 3: Naming and error-handling cleanup
   - Pass 4: Test reinforcement
3. Use eval-harness benchmarks as regression protection during cleanup
4. Check ADRs before removing abstractions that may be deliberate

**Output checkpoint**: Clean, production-grade code with all regression tests passing

**On failure**: If cleanup introduces regressions that cannot be fixed, revert the cleanup pass and report. The self-improve output remains valid.

### Step 6: Acceptance Check — Goal Met?

After Phase 5, run the benchmark from Phase 3 and compare against the acceptance criteria.

**Evaluation**:
1. Run the benchmark command on the current code
2. Compare the score against the acceptance criteria defined in Phase 3
3. Determine the outcome:

| Outcome | Condition | Action |
|---|---|---|
| **Goal met** | Score meets or exceeds acceptance criteria | → Step 7: Deliver Results |
| **Making progress** | Score improved but not yet at target | → Re-enter at Phase 4 with new ideas |
| **Stuck / Plateau** | Score stopped improving across multiple cycles | → Trigger Phase 6 (external-research), then re-enter loop |
| **Regressed** | Score dropped after cleanup | → Revert cleanup, re-enter at Phase 4 |

**On re-entry to Phase 4 (making progress)**:
- Write new strategy ideas to `<self-improve-root>/config/idea.md`
- Update pipeline state: increment `cycle_count`
- Continue the loop

**On bottleneck detected (stuck / plateau)**:
- Check trigger condition: `cycle_count >= 10` AND no improvement in last 5 cycles
- If triggered: invoke `external-research` skill (Phase 6) — see "Bottleneck Detection & External Research (Phase 6)" above
- After external-research completes: re-enter at Phase 4 (incremental ideas) or Phase 1 (fundamentally different approach)
- If NOT triggered (plateau but not yet at 10 cycles): re-enter at Phase 1 to re-plan with internal knowledge
- Update pipeline state: increment `cycle_count`, set `bottleneck_detected`

**Loop safety**:
- No cycle limit — the pipeline runs as long as needed
- Bottleneck detection: if the score has not improved for 5 cycles and cycle_count >= 10, trigger Phase 6 (external-research)
- User can stop the pipeline at any time

### Step 7: Deliver Results

Present the final summary to the user:

```
=== AI Pipeline Complete ===

Goal: {original objective}
Repository: {repo path}
Pipeline cycles: {cycle_count}

Phase 1 (Blueprint): ✅ {N} steps planned
Phase 2 (ADR): ✅ {N} decisions recorded
Phase 3 (Eval Harness): ✅ Baseline {score}, benchmark ready
Phase 4 (Self-Improve): ✅ {total_iterations} iterations across {cycle_count} cycles
Phase 5 (Slop Cleaner): ✅ {N} files cleaned

Final Results:
- Baseline score: {baseline}
- Final score: {final_score}
- Improvement: {delta} ({delta_pct}%)
- Acceptance criteria: {criteria} — MET ✅

Artifacts:
- Improvement branch: improve/{goal_slug}
- ADRs: docs/adr/
- Evals: .trae/evals/
- Progress chart: .trae/self-improve/topics/{slug}/tracking/progress.png
- Pipeline state: .trae/pipeline-state.json

Next steps:
- Review the improvement branch: git checkout improve/{goal_slug}
- Create a PR: gh pr create --head improve/{goal_slug} --base {target_branch}
- Or merge directly: git checkout {target_branch} && git merge improve/{goal_slug}
```

## Failure Strategy

| Situation | Action |
|---|---|
| Blueprint fails | Go back to Step 0, ask more clarifying questions. Do NOT proceed with a weak plan. |
| ADR fails | Log warning, continue. Non-blocking. |
| Eval-harness fails (no benchmark) | Ask user for benchmark command. If unavailable, exit — the loop requires quantifiable criteria. |
| Self-improve fails to start | Skip to slop-cleaner with current code, then do acceptance check. |
| Self-improve crashes mid-loop | Resume from last checkpoint on re-invocation. |
| Slop-cleaner introduces regression | Revert the cleanup pass. Self-improve output remains. |
| Acceptance check shows regression | Revert cleanup, re-enter Phase 4. |
| Bottleneck detected (5 cycles no improvement) | Trigger Phase 6 (external-research skill), inject new ideas, continue loop. |
| User stops pipeline | Record state, exit gracefully. Can resume later. |

## Pipeline State Tracking

Track pipeline progress in `.trae/pipeline-state.json`:

```json
{
  "objective": "user's original goal",
  "repo_path": "/path/to/repo",
  "topic_slug": "derived-slug",
  "started_at": "ISO 8601",
  "current_phase": 4,
  "cycle_count": 2,
  "replan_count": 0,
  "last_external_research_cycle": 0,
  "bottleneck_detected": false,
  "acceptance_criteria": {
    "metric": "primary",
    "target_value": 95.0,
    "direction": "higher_is_better"
  },
  "current_score": 88.5,
  "baseline_score": 72.0,
  "phases": {
    "blueprint": { "status": "completed", "output_path": "plans/...", "completed_at": "..." },
    "adr": { "status": "completed", "output_path": "docs/adr/", "completed_at": "..." },
    "eval_harness": { "status": "completed", "baseline_score": 72.0, "completed_at": "..." },
    "self_improve": { "status": "completed", "best_score": 88.5, "iterations": 12, "completed_at": "..." },
    "slop_cleaner": { "status": "completed", "completed_at": "..." },
    "external_research": { "status": "not_triggered", "last_triggered_cycle": null, "ideas_generated": 0, "completed_at": null }
  },
  "loop_history": [
    { "cycle": 1, "entry_phase": 1, "score_before": 72.0, "score_after": 85.0, "outcome": "making_progress" },
    { "cycle": 2, "entry_phase": 4, "score_before": 85.0, "score_after": 88.5, "outcome": "making_progress" }
  ],
  "completed_at": null
}
```

On re-invocation, check this file to resume from the last completed phase and cycle.

## Resumability

If the pipeline is interrupted:
1. Read `.trae/pipeline-state.json`
2. Find the last completed phase and cycle
3. Resume from the next phase in the current cycle
4. Each individual skill (especially self-improve) has its own resumability mechanism
5. If the pipeline was in a loop, resume the loop at the appropriate entry point