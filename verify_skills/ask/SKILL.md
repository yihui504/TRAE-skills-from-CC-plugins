---
name: ask
description: "Process-first advisor routing via TRAE IDE's agent capabilities, with artifact capture and no raw CLI assembly"
---

# ask

# Ask

Use TRAE IDE's agent capabilities to route a prompt through the appropriate intelligent agent and persist the result as an ask artifact.

## Usage

```
 <agent-type> <question or task>
```

Examples:

```
 @backend-architect "review this patch from a security perspective"
 @frontend-architect "suggest UX improvements for this flow"
 @backend-architect "draft an implementation plan for issue #123"
```

## Routing

**Required execution path — always use TRAE IDE's agent capabilities:**

Call the appropriate intelligent agent directly (e.g., @backend-architect, @frontend-architect, @search). **Do NOT manually construct raw provider CLI commands.** TRAE IDE's agent system handles correct flag selection, artifact persistence, and compatibility automatically. Manually assembling provider CLI flags will produce incorrect or outdated invocations.

## Requirements

- The selected intelligent agent must be available in the current TRAE IDE environment.

## Artifacts

Agent call results write artifacts to:

```text
.trae/artifacts/ask/--.md
```

Task:
