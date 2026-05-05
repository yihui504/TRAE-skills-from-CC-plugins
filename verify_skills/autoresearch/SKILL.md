---
name: autoresearch
description: Stateful single-mission improvement loop with strict evaluator contract, markdown decision logs, and max-runtime stop behavior
---

# autoresearch

## 描述

Autoresearch is a stateful skill for bounded, evaluator-driven iterative improvement. It owns one mission at a time, keeps iterating through non-passing results, records each evaluation and decision as durable artifacts, and stops only when an explicit max-runtime ceiling or another explicit terminal condition is reached.

## 使用场景

- You already have a mission and evaluator from `/deep-interview --autoresearch`
- You want persistent single-mission improvement with strict evaluation
- You need durable experiment logs under `.trae/autoresearch/`
- You want a supported path for periodic reruns via TRAE IDE 定时任务

## 不适用场景

- You need evaluator generation at runtime — use `/deep-interview --autoresearch` first
- You need multiple missions orchestrated together — v1 forbids that
- You want the deprecated CLI flow — it is no longer authoritative


- Single-mission only in v1
- Mission setup/evaluator generation stays in `deep-interview --autoresearch`
- Evaluator output must be structured JSON with required boolean `pass` and optional numeric `score`
- Non-passing iterations do **not** stop the run
- Stop conditions are explicit and bounded, with max-runtime as the primary strict stop hook


Canonical persistent storage lives under `.trae/autoresearch//` and/or `.trae/logs/autoresearch//`.

Minimum required artifacts:
- mission spec
- evaluator script or command reference
- per-iteration evaluation JSON
- markdown decision logs

Recommended canonical shape:
```text
.trae/autoresearch//
  mission.md
  evaluator.json
  runs//
    evaluations/
      iteration-0001.json
      iteration-0002.json
    decision-log.md
```
Reuse existing runtime artifacts when available rather than duplicating them unnecessarily.


1. Confirm a single mission exists and evaluator setup is already available.
2. Ensure mode/state is active for `autoresearch` and records:
   - mission slug/dir
   - evaluator reference
   - iteration count
   - started/updated timestamps
   - explicit max-runtime or deadline
3. On every iteration:
   - run exactly one experiment/change cycle
   - run the evaluator
   - persist machine-readable evaluation JSON
   - append a human-readable markdown decision log entry
   - continue even when evaluation does not pass
4. Stop when:
   - max-runtime ceiling is reached
   - user explicitly cancels
   - another explicit terminal condition is recorded by the runtime


TRAE IDE 定时任务 is a supported integration point for periodic mission enhancement. In v1, prefer documenting/configuring cron inputs over building a large scheduler UI.

If cron is used:
- keep one mission per scheduled job
- preserve the same mission/evaluator contract
- append new run artifacts rather than overwriting prior experiments


## 执行策略

- Do not hand execution back to deprecated CLI flows
- Do not create multi-mission orchestration
- Prefer reusing `src/autoresearch/*` runtime/schema helpers where they already match the stricter contract
- Keep logs useful to humans, not only machines