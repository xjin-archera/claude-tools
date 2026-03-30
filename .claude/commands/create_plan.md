---
description: Create detailed implementation plans through interactive research and iteration
model: opus
---

# Implementation Plan

You are tasked with creating detailed implementation plans through an interactive, iterative process. You should be skeptical, thorough, and work collaboratively with the user to produce high-quality technical specifications.

## Initial Response

When this command is invoked:

1. **Check if parameters were provided**:
   - If a file path or ticket reference was provided as a parameter, skip the default message
   - Immediately read any provided files FULLY
   - Begin the research process

2. **If no parameters provided**, respond with:
```
I'll help you create a detailed implementation plan. Let me start by understanding what we're building.

Please provide:
1. The task/ticket description (or reference to a ticket file)
2. Any relevant context, constraints, or specific requirements
3. Links to related research or previous implementations

I'll analyze this information and work with you to create a comprehensive plan.

Tip: You can also invoke this command with a ticket file directly: `/create_plan thoughts/xifengjin/tickets/ARS-1234.md`
For deeper analysis, try: `/create_plan think deeply about thoughts/xifengjin/tickets/ARS-1234.md`
```

Then wait for the user's input.

## Process Steps

### Step 1: Context Gathering & Initial Analysis

1. **Read all mentioned files immediately and FULLY**:
   - Ticket files (e.g., `thoughts/xifengjin/tickets/ARS-1234.md`)
   - Research documents
   - Related implementation plans
   - **IMPORTANT**: Use the Read tool WITHOUT limit/offset parameters to read entire files
   - **CRITICAL**: DO NOT spawn sub-tasks before reading these files yourself in the main context

2. **Spawn initial research tasks to gather context**:
   Before asking the user any questions, use specialized agents to research in parallel:

   - Use the **codebase-locator** agent to find all files related to the ticket/task
   - Use the **codebase-analyzer** agent to understand how the current implementation works
   - If relevant, use the **thoughts-locator** agent to find any existing thoughts documents about this feature

   These agents will:
   - Find relevant source files, configs, and tests
   - Identify the specific directories to focus on
   - Trace data flow and key functions
   - Return detailed explanations with file:line references

3. **Read all files identified by research tasks**:
   - After research tasks complete, read ALL files they identified as relevant
   - Read them FULLY into the main context

4. **Analyze and verify understanding**:
   - Cross-reference the ticket requirements with actual code
   - Identify any discrepancies or misunderstandings
   - Note assumptions that need verification

5. **Present informed understanding and focused questions**:
   ```
   Based on the ticket and my research of the codebase, I understand we need to [accurate summary].

   I've found that:
   - [Current implementation detail with file:line reference]
   - [Relevant pattern or constraint discovered]
   - [Potential complexity or edge case identified]

   Questions that my research couldn't answer:
   - [Specific technical question that requires human judgment]
   - [Business logic clarification]
   - [Design preference that affects implementation]
   ```

   Only ask questions that you genuinely cannot answer through code investigation.

### Step 2: Research & Discovery

After getting initial clarifications:

1. **If the user corrects any misunderstanding**:
   - DO NOT just accept the correction
   - Spawn new research tasks to verify the correct information
   - Only proceed once you've verified the facts yourself

2. **Create a research todo list** using TodoWrite to track exploration tasks

3. **Spawn parallel sub-tasks for comprehensive research**:

   **For deeper investigation:**
   - **codebase-locator** - To find more specific files
   - **codebase-analyzer** - To understand implementation details
   - **codebase-pattern-finder** - To find similar features we can model after

   **For historical context:**
   - **thoughts-locator** - To find any research, plans, or decisions about this area
   - **thoughts-analyzer** - To extract key insights from relevant documents

4. **Present findings and design options**

### Step 3: Plan Structure Development

Once aligned on approach, present a plan outline and get feedback before writing details.

### Step 4: Detailed Plan Writing

After structure approval, write the plan to:
`thoughts/shared/plans/YYYY-MM-DD-ARS-XXXX-description.md`

Use this template:

````markdown
# [Feature/Task Name] Implementation Plan

## Overview

[Brief description of what we're implementing and why]

## Current State Analysis

[What exists now, what's missing, key constraints discovered]

## Desired End State

[Specification of the desired end state and how to verify it]

### Key Discoveries:
- [Important finding with file:line reference]
- [Pattern to follow]
- [Constraint to work within]

## What We're NOT Doing

[Explicitly list out-of-scope items to prevent scope creep]

## Implementation Approach

[High-level strategy and reasoning]

## Phase 1: [Descriptive Name]

### Overview
[What this phase accomplishes]

### Changes Required:

#### 1. [Component/File Group]
**File**: `path/to/file.ext`
**Changes**: [Summary of changes]

```python
# or typescript — specific code to add/modify
```

### Success Criteria:

#### Automated Verification:
- [ ] Backend lint passes: `cd server && make lint`
- [ ] Backend tests pass: `cd server && uv run pytest -s path/to/test.py`
- [ ] Frontend lint passes: `cd web && make lint`
- [ ] TypeScript types valid: `cd web && make validate-types`
- [ ] Frontend tests pass: `cd web && make test`

#### Manual Verification:
- [ ] Feature works as expected when tested via UI
- [ ] No regressions in related features

**Implementation Note**: After completing this phase and all automated verification passes, pause here for manual confirmation from the human before proceeding to the next phase.

---

## Phase 2: [Descriptive Name]

[Similar structure...]

---

## Testing Strategy

### Backend Tests:
- [What to test]
- [Key edge cases]

### Frontend Tests:
- [Component tests]
- [Integration scenarios]

### Manual Testing Steps:
1. [Specific step to verify feature]
2. [Another verification step]

## Migration Notes

[If applicable — Alembic migrations, Snowflake migrations, data backfills]

## References

- Original ticket: `thoughts/xifengjin/tickets/ARS-XXXX.md`
- Related research: `thoughts/shared/research/[relevant].md`
- Similar implementation: `[file:line]`
````

### Step 5: Review

1. **Present the draft plan location**
2. **Iterate based on feedback**
3. **Continue refining** until the user is satisfied

## Important Guidelines

1. **Be Skeptical**: Question vague requirements, verify with code
2. **Be Interactive**: Don't write the full plan in one shot, get buy-in at each step
3. **Be Thorough**: Read all context files completely before planning
4. **Be Practical**: Focus on incremental, testable changes
5. **Track Progress**: Use TodoWrite to track planning tasks
6. **No Open Questions in Final Plan**: Every decision must be made before finalizing

## Common Patterns for This Codebase

### For Backend Changes (server/):
- Start with Alembic migration (if schema changes)
- Add/update SQLAlchemy models
- Add business logic in `server/src/reservedai/`
- Add/update API endpoint in `server/src/app/api/{internal|public|partners}/`
- Add/update Marshmallow schema
- Write pytest tests

### For Frontend Changes (web/):
- Start with TypeScript types (or regenerate from OpenAPI: `cd web && make ts-regen`)
- Add API service call in `web/src/_services/`
- Add Redux slice if needed in `web/src/_redux/`
- Implement React component/page in `web/src/_pages/` or `web/src/_components/`
- Write Vitest tests

### For Full-Stack Features:
- Backend first, then frontend
- Regenerate OpenAPI types after backend changes
