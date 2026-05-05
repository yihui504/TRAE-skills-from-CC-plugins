---
name: ask
description: "Process-first advisor routing for Claude, Codex, or Gemini via `omc ask`, with artifact capture and no raw CLI assembly"
---

# ask

# Ask

Use OMC's canonical advisor skill to route a prompt through the local Claude, Codex, or Gemini CLI and persist the result as an ask artifact.

## Usage

```bash
 <claude|codex|gemini> <question or task>
```

Examples:

```bash
 codex "review this patch from a security perspective"
 gemini "suggest UX improvements for this flow"
 claude "draft an implementation plan for issue #123"
```

## Routing

**Required execution path — always use this command:**

```bash
omc ask 
```

**Do NOT manually construct raw provider CLI commands.** Never run `codex`, `claude`, or `gemini` directly to fulfill this skill. The `omc ask` wrapper handles correct flag selection, artifact persistence, and provider-version compatibility automatically. Manually assembling provider CLI flags will produce incorrect or outdated invocations.

## Requirements

- The selected local CLI must be installed and authenticated.
- Verify availability with the matching command:

```bash
claude --version
codex --version
gemini --version
```

## Artifacts

`omc ask` writes artifacts to:

```text
.trae/artifacts/ask/--.md
```

Task: