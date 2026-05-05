---
name: external-context
description: Invoke parallel document-specialist agents for external web searches and documentation lookup
---

# external-context

# External Context Skill

Fetch external documentation, references, and context for a query. Decomposes into 2-5 facets and spawns parallel document-specialist Claude agents.

## Usage

```
-context <topic or question>
```

### Examples

```
-context What are the best practices for JWT token rotation in Node.js?
-context Compare Prisma vs Drizzle ORM for PostgreSQL
-context Latest React Server Components patterns and conventions
```

## Protocol

### Step 1: Facet Decomposition

Given a query, decompose into 2-5 independent search facets:

```markdown
## Search Decomposition

**Query:** <original query>

### Facet 1: 
- **Search focus:** What to search for
- **Sources:** Official docs, GitHub, blogs, etc.

### Facet 2: 
...
```

### Step 2: Parallel Agent Invocation

通过智能体调用并行发射独立搜索面：

```
调用 @-specialist 智能体, prompt="Search for: <facet 1 description>. Use WebSearch and WebFetch to find official documentation and examples. Cite all sources with URLs."

调用 @-specialist 智能体, prompt="Search for: <facet 2 description>. Use WebSearch and WebFetch to find official documentation and examples. Cite all sources with URLs."
```

Maximum 5 parallel document-specialist agents.

### Step 3: Synthesis Output Format

Present synthesized results in this format:

```markdown
## External Context: 

### Key Findings
1. **** - Source: [title](url)
2. **** - Source: [title](url)

### Detailed Results

#### Facet 1: 
<aggregated findings with citations>

#### Facet 2: 
<aggregated findings with citations>

### Sources
- [Source 1](url)
- [Source 2](url)
```

## Configuration

- Maximum 5 parallel document-specialist agents
- No magic keyword trigger - explicit invocation only