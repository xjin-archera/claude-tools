---
description: Create implementation plans with thorough research (no thoughts directory)
model: opus
---

# Implementation Plan (No Thoughts Directory)

You are tasked with creating detailed implementation plans through an interactive, iterative process. This variant does not use the thoughts/ directory — plans are saved locally or shown inline.

## Initial Response

When this command is invoked:

1. **Check if parameters were provided**:
   - If a file path or ticket reference was provided, read it FULLY and begin research
   - If no parameters, respond with:

```
I'll help you create a detailed implementation plan. Let me start by understanding what we're building.

Please provide:
1. The task/ticket description or Jira ticket reference (ARS-XXXX)
2. Any relevant context, constraints, or specific requirements
3. Links to related research or previous implementations
```

Then wait for input.

## Process Steps

### Step 1: Context Gathering & Initial Analysis

1. **Read all mentioned files immediately and FULLY** (no limit/offset)
2. **Spawn initial research tasks in parallel**:
   - **codebase-locator** — find all files related to the task
   - **codebase-analyzer** — understand current implementation
   - **codebase-pattern-finder** — find similar patterns to model after
3. **Read all files identified by research tasks**
4. **Present informed understanding and focused questions**

### Step 2: Research & Discovery

Spawn parallel sub-tasks as needed:
- **codebase-locator**, **codebase-analyzer**, **codebase-pattern-finder**

Present findings and design options before proceeding.

### Step 3: Plan Structure Development

Present a plan outline and get feedback before writing details.

### Step 4: Detailed Plan Writing

Write the plan (to a local file or show inline):

````markdown
# [Feature/Task Name] Implementation Plan

## Overview
[Brief description of what we're implementing and why]

## Current State Analysis
[What exists now, what's missing, key constraints]

## Desired End State
[Specification of the desired end state and how to verify it]

### Key Discoveries:
- [Important finding with file:line reference]

## What We're NOT Doing
[Explicitly list out-of-scope items]

## Implementation Approach
[High-level strategy and reasoning]

## Phase 1: [Descriptive Name]

### Overview
[What this phase accomplishes]

### Changes Required:

#### 1. [Component/File Group]
**File**: `path/to/file.ext`
**Changes**: [Summary]

```python
# Specific code to add/modify
```

### Success Criteria:

#### Automated Verification:
- [ ] Backend lint: `cd server && make lint`
- [ ] Backend tests: `cd server && uv run pytest -s path/to/test.py`
- [ ] Frontend lint: `cd web && make lint`
- [ ] TypeScript types: `cd web && make validate-types`
- [ ] Frontend tests: `cd web && make test`

#### Manual Verification:
- [ ] Feature works as expected via UI
- [ ] No regressions in related features

**Implementation Note**: Pause after automated verification for manual confirmation before proceeding.

---

## Phase 2: [Descriptive Name]
[Similar structure...]

## Testing Strategy

### Backend Tests (pytest):
- [What to test, key edge cases]

### Frontend Tests (Vitest):
- [Component and integration scenarios]

### Manual Testing Steps:
1. [Specific verification step]

## Migration Notes
[Alembic / Snowflake migrations if applicable]

## References
- Jira ticket: ARS-XXXX
- Similar implementation: `[file:line]`
````

### Step 5: Review

Present the plan, iterate based on feedback until user is satisfied.

## Important Guidelines

1. **Be Skeptical**: Verify with code, don't assume
2. **Be Interactive**: Get buy-in at each major step
3. **Be Thorough**: Read all context files completely
4. **No Open Questions in Final Plan**: Every decision must be resolved

## Common Patterns for This Codebase

### Backend (server/):
- Alembic migration → SQLAlchemy model → business logic → API endpoint → Marshmallow schema → pytest tests

### Frontend (web/):
- Regenerate OpenAPI types → API service → Redux slice (if needed) → React component → Vitest tests

### Full-Stack:
- Backend first → regenerate types → frontend
