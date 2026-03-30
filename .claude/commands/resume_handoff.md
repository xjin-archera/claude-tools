---
description: Resume work from handoff document with context analysis and validation
---

# Resume Work from a Handoff Document

You are tasked with resuming work from a handoff document. These contain critical context, learnings, and next steps from previous sessions.

## Initial Response

1. **If a handoff file path was provided**:
   - Read the handoff document FULLY
   - Read any plan or research documents it links to (do NOT use a sub-agent for this)
   - Begin the analysis process
   - Propose a course of action and confirm with the user

2. **If a ticket number (ARS-XXXX) was provided**:
   - Locate the most recent handoff: list `thoughts/shared/handoffs/ARS-XXXX/`
   - If directory is empty or missing: "I can't find a handoff for that ticket. Please provide the path."
   - If one file: proceed with it
   - If multiple files: use the most recent based on `YYYY-MM-DD_HH-MM-SS` in the filename
   - Read the handoff and linked documents FULLY
   - Propose a course of action

3. **If no parameters provided**:
   ```
   I'll help you resume work from a handoff document.

   Please provide either:
   - A path to the handoff file: `/resume_handoff thoughts/shared/handoffs/ARS-XXXX/YYYY-MM-DD_HH-MM-SS_ARS-XXXX_description.md`
   - A Jira ticket number: `/resume_handoff ARS-XXXX`
   ```

## Process Steps

### Step 1: Read and Analyze Handoff

1. **Read handoff document completely** (no limit/offset)
2. **Extract all sections**: tasks, recent changes, learnings, artifacts, action items
3. **Spawn focused research tasks** to verify current state:
   - Read all artifacts mentioned in the handoff
   - Read implementation plans and research documents referenced
   - Verify that recent changes are still present in the codebase

### Step 2: Synthesize and Present Analysis

```
I've analyzed the handoff from [date]. Here's the current situation:

**Original Tasks:**
- [Task 1]: [Status from handoff] → [Current verification]

**Key Learnings Validated:**
- [Learning with file:line] — Still valid / Changed

**Recent Changes Status:**
- [Change 1] — Verified present / Missing / Modified

**Artifacts Reviewed:**
- [Document 1]: [Key takeaway]

**Recommended Next Actions:**
1. [Most logical next step]
2. [Second priority]

Shall I proceed with [recommended action 1], or would you like to adjust the approach?
```

Get confirmation before proceeding.

### Step 3: Create Action Plan

Use TodoWrite to create a task list:
- Convert action items from handoff into todos
- Add any new tasks discovered during analysis
- Prioritize based on dependencies and handoff guidance

### Step 4: Begin Implementation

- Start with the first approved task
- Reference learnings from handoff throughout implementation
- Apply patterns and approaches documented in the handoff

## Guidelines

1. **Read entire handoff + all referenced artifacts** before starting
2. **Never assume handoff state matches current state** — verify all file references
3. **Pay special attention to "Learnings"** — apply documented patterns, avoid documented mistakes
4. **Use TodoWrite** to maintain task continuity
5. **Consider creating a new handoff** when done if work continues to another session

## Common Scenarios

- **Clean Continuation**: All changes present, clear next steps → proceed
- **Diverged Codebase**: Some changes missing or modified → reconcile differences
- **Incomplete Work**: Tasks marked "in progress" → complete before starting new work
- **Stale Handoff**: Major time has passed or refactoring occurred → re-evaluate strategy
