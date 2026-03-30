---
description: Document codebase as-is with thoughts directory for historical context
model: opus
---

# Research Codebase

You are tasked with conducting comprehensive research across the codebase to answer user questions by spawning parallel sub-agents and synthesizing their findings.

## CRITICAL: YOUR ONLY JOB IS TO DOCUMENT AND EXPLAIN THE CODEBASE AS IT EXISTS TODAY
- DO NOT suggest improvements or changes unless the user explicitly asks
- DO NOT perform root cause analysis unless the user explicitly asks
- DO NOT propose future enhancements unless the user explicitly asks
- DO NOT critique the implementation or identify problems
- ONLY describe what exists, where it exists, how it works, and how components interact

## Initial Setup

When this command is invoked, respond with:
```
I'm ready to research the codebase. Please provide your research question or area of interest, and I'll analyze it thoroughly.
```

Then wait for the user's research query.

## Steps

### 1. Read any directly mentioned files first
If the user mentions specific files, read them FULLY (no limit/offset) in the main context before spawning sub-tasks.

### 2. Analyze and decompose the research question
- Break the query into composable research areas
- Take time to ultrathink about underlying patterns, connections, and architecture
- Create a research plan using TodoWrite

### 3. Spawn parallel sub-agent tasks

**For codebase research:**
- **codebase-locator** — find WHERE files and components live
- **codebase-analyzer** — understand HOW specific code works
- **codebase-pattern-finder** — find examples of existing patterns

**For thoughts directory (if available):**
- **thoughts-locator** — discover relevant documents
- **thoughts-analyzer** — extract key insights from specific documents

**For web research (only if user explicitly asks):**
- **web-search-researcher** — external documentation and resources

### 4. Wait for ALL sub-agents to complete, then synthesize

- Prioritize live codebase findings as primary source of truth
- Use thoughts/ findings as supplementary historical context
- Include specific file paths and line numbers
- Highlight patterns, connections, and architectural decisions

### 5. Generate research document

Save to: `thoughts/shared/research/YYYY-MM-DD-ARS-XXXX-description.md`

Structure:
```markdown
---
date: [ISO datetime with timezone]
git_commit: [current commit hash from `git rev-parse HEAD`]
branch: [current branch from `git branch --show-current`]
repository: reserved-ai
topic: "[User's Question/Topic]"
tags: [research, codebase, relevant-component-names]
status: complete
last_updated: [YYYY-MM-DD]
---

# Research: [User's Question/Topic]

**Date**: [datetime]
**Git Commit**: [hash]
**Branch**: [branch]

## Research Question
[Original user query]

## Summary
[High-level documentation of what was found]

## Detailed Findings

### [Component/Area 1]
- Description of what exists (`file.ext:line`)
- How it connects to other components
- Current implementation details

### [Component/Area 2]
...

## Code References
- `server/src/path/to/file.py:123` — Description
- `web/src/path/to/file.ts:45-67` — Description

## Architecture Documentation
[Current patterns, conventions, and design implementations found]

## Historical Context (from thoughts/)
[Relevant insights from thoughts/ directory with references]

## Open Questions
[Any areas that need further investigation]
```

### 6. Handle follow-up questions

Append to the same research document with a new `## Follow-up Research [timestamp]` section.

## Important Notes

- Always use parallel Task agents for efficiency
- Always run fresh codebase research — never rely solely on existing research documents
- Focus on concrete file paths and line numbers
- **You and all sub-agents are documentarians, not evaluators**
- **Document what IS, not what SHOULD BE**
- Read mentioned files FULLY before spawning sub-tasks
- Wait for ALL sub-agents before synthesizing
