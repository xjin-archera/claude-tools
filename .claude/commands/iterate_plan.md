---
description: Iterate on existing implementation plans with thorough research and updates
model: opus
---

# Iterate Implementation Plan

You are tasked with updating existing implementation plans based on user feedback. Be skeptical, thorough, and ensure changes are grounded in actual codebase reality.

## Initial Response

1. **Parse the input to identify**:
   - Plan file path (e.g., `thoughts/shared/plans/2025-01-08-ARS-1234-description.md`)
   - Requested changes/feedback

2. **Handle different input scenarios**:

   **If NO plan file provided**:
   ```
   I'll help you iterate on an existing implementation plan.
   Which plan would you like to update? Please provide the path to the plan file.
   Tip: You can list recent plans with `ls -lt thoughts/shared/plans/ | head`
   ```

   **If plan file provided but NO feedback**:
   ```
   I've found the plan at [path]. What changes would you like to make?
   For example:
   - "Add a phase for migration handling"
   - "Update the success criteria to include performance tests"
   - "Split Phase 2 into backend and frontend phases"
   ```

   **If BOTH plan file AND feedback provided**: Proceed immediately.

## Process Steps

### Step 1: Read and Understand Current Plan

1. **Read the existing plan file COMPLETELY** (no limit/offset)
2. **Understand the requested changes**: what to add/modify/remove, scope of the update

### Step 2: Research If Needed

Only spawn research tasks if changes require new technical understanding:

1. Use TodoWrite to track research tasks
2. Spawn parallel sub-tasks as needed:
   - **codebase-locator** — find relevant files
   - **codebase-analyzer** — understand implementation details
   - **codebase-pattern-finder** — find similar patterns
   - **thoughts-locator** / **thoughts-analyzer** — find historical context
3. Read any new files identified by research FULLY
4. Wait for ALL sub-tasks to complete

### Step 3: Present Understanding and Approach

Before making changes, confirm your understanding:

```
Based on your feedback, I understand you want to:
- [Change 1 with specific detail]
- [Change 2 with specific detail]

My research found:
- [Relevant code pattern or constraint]
- [Important discovery that affects the change]

I plan to update the plan by:
1. [Specific modification to make]
2. [Another modification]

Does this align with your intent?
```

Get user confirmation before proceeding.

### Step 4: Update the Plan

1. **Make focused, precise edits** using the Edit tool
2. **Ensure consistency**:
   - New phases follow the existing pattern
   - Update "What We're NOT Doing" if scope changes
   - Maintain distinction between automated vs manual success criteria
3. **Preserve quality standards**:
   - Keep specific file paths and line numbers
   - Use `make` commands for automated verification
   - Keep language clear and actionable

### Step 5: Review

Present the changes made and invite further feedback.

## Important Guidelines

1. **Be Skeptical**: Don't blindly accept change requests, verify technical feasibility
2. **Be Surgical**: Make precise edits, not wholesale rewrites
3. **Be Thorough**: Read entire plan before making changes
4. **Be Interactive**: Confirm understanding before acting
5. **No Open Questions**: Every change must be complete and actionable

## Success Criteria Structure

Always maintain:

**Automated Verification** (can be run):
- `cd server && make lint`
- `cd server && uv run pytest -s path/to/test.py`
- `cd web && make lint`
- `cd web && make validate-types`
- `cd web && make test`

**Manual Verification** (requires human testing):
- UI/UX functionality
- Performance under real conditions
- User acceptance criteria
