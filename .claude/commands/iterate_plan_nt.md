---
description: Iterate on existing implementation plans (no thoughts directory)
model: opus
---

# Iterate Implementation Plan (No Thoughts Directory)

Same as iterate_plan.md but for use when the thoughts/ directory is not available.
Plans are read from and written to local files or shown inline.

## Initial Response

Parse input for plan file path and requested changes. If either is missing, ask for it.

## Process Steps

### Step 1: Read and Understand Current Plan
Read the plan file COMPLETELY (no limit/offset). Parse what needs to change.

### Step 2: Research If Needed

Only spawn research tasks if changes require new technical understanding:
- **codebase-locator**, **codebase-analyzer**, **codebase-pattern-finder**

### Step 3: Present Understanding and Confirm

```
Based on your feedback, I understand you want to:
- [Change 1]
- [Change 2]

I plan to update the plan by:
1. [Specific modification]

Does this align with your intent?
```

### Step 4: Update the Plan

Use the Edit tool for surgical changes. Maintain:
- Existing structure unless explicitly changing it
- File:line references (keep them accurate)
- Automated vs manual success criteria distinction

**Automated Verification commands for this codebase:**
- `cd server && make lint`
- `cd server && uv run pytest -s path/to/test.py`
- `cd web && make lint`
- `cd web && make validate-types`
- `cd web && make test`

### Step 5: Review

Present the changes made and invite further feedback.

## Guidelines

- **Be Surgical**: Precise edits, not rewrites
- **Be Skeptical**: Verify feasibility with code research
- **No Open Questions**: Resolve all ambiguity before updating
- **Keep quality**: file:line references, measurable criteria, clear language
