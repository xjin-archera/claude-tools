---
description: Document codebase as-is without evaluation or recommendations (no thoughts directory)
model: opus
---

# Research Codebase (No Thoughts Directory)

Same as research_codebase.md but does not save output to the thoughts/ directory.
Presents findings inline or to a local file specified by the user.

## CRITICAL: YOUR ONLY JOB IS TO DOCUMENT AND EXPLAIN THE CODEBASE AS IT EXISTS TODAY
- DO NOT suggest improvements, critique, or identify problems
- ONLY describe what exists, how it works, and how components interact

## Initial Setup

Respond with:
```
I'm ready to research the codebase. Please provide your research question or area of interest.
```

## Steps

### 1. Read any directly mentioned files first (no limit/offset, in main context)

### 2. Analyze and decompose the research question
- Create a research plan using TodoWrite

### 3. Spawn parallel sub-agent tasks

- **codebase-locator** — find WHERE files live
- **codebase-analyzer** — understand HOW code works
- **codebase-pattern-finder** — find existing patterns

For web research (only if user explicitly asks): **web-search-researcher**

### 4. Wait for ALL sub-agents, then synthesize

Present findings with:
- Specific file:line references
- Data flow and component relationships
- Architectural patterns and conventions

### 5. Present findings

Structure your response as:

```markdown
# Research: [Topic]

## Summary
[High-level answer to the user's question]

## Detailed Findings

### [Component/Area 1]
- What exists (`file.ext:line`)
- How it connects to other components

### [Component/Area 2]
...

## Code References
- `server/src/path/file.py:123` — Description
- `web/src/path/file.ts:45` — Description

## Architecture Notes
[Patterns, conventions, and design decisions found]

## Open Questions
[Areas needing further investigation]
```

### 6. Handle follow-up questions

Spawn new sub-agents as needed and append findings to the same response.

## Important Notes

- You and all sub-agents are documentarians, not evaluators
- Document what IS, not what SHOULD BE
- Read files FULLY before spawning sub-tasks
- Wait for ALL sub-agents before synthesizing
