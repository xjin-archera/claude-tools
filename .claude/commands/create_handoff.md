---
description: Create handoff document for transferring work to another session
---

# Create Handoff

You are tasked with writing a handoff document to transfer your work to another agent in a new session. Be thorough but concise — compact and summarize context without losing key details.

## Process

### 1. Filepath & Metadata

Create your file at:
`thoughts/shared/handoffs/ARS-XXXX/YYYY-MM-DD_HH-MM-SS_ARS-XXXX_description.md`

Where:
- `YYYY-MM-DD` is today's date
- `HH-MM-SS` is current time in 24-hour format
- `ARS-XXXX` is the Jira ticket number (use `general` if no ticket)
- `description` is a brief kebab-case description

Run these to gather metadata:
```bash
git rev-parse HEAD          # commit hash
git branch --show-current   # branch name
date -u +"%Y-%m-%dT%H:%M:%SZ"  # current datetime
```

Examples:
- With ticket: `2025-03-30_13-55-22_ARS-14813_add-anomaly-detail-card.md`
- Without ticket: `2025-03-30_13-55-22_general_fix-auth-flow.md`

### 2. Write the Handoff Document

```markdown
---
date: [ISO datetime with timezone]
git_commit: [current commit hash]
branch: [current branch name]
repository: reserved-ai
topic: "[Feature/Task Name] Implementation Strategy"
tags: [implementation, strategy, relevant-component-names]
status: complete
last_updated: [YYYY-MM-DD]
---

# Handoff: ARS-XXXX {very concise description}

## Task(s)
{Description of tasks worked on, along with status of each (completed, work in progress, planned/discussed).
If working from an implementation plan, call out which phase you are on.
Reference any plan or research documents you worked from.}

## Critical References
{2-3 most important file paths that must be read to understand the work.}

## Recent Changes
{Describe recent changes made to the codebase using file:line syntax.}

## Learnings
{Important things learned — patterns, root causes of bugs, gotchas.
Include explicit file paths and line numbers where relevant.}

## Artifacts
{Exhaustive list of artifacts produced or updated as filepaths and/or file:line references —
e.g. paths to feature documents, implementation plans, etc. that should be read to resume work.}

## Action Items & Next Steps
{List of action items and next steps for the next agent based on task statuses.}

## Other Notes
{Other notes, references, or useful information that doesn't fit above — e.g. where relevant
sections of the codebase are, or other important things learned.}
```

### 3. Confirm and Save

After writing the document, respond to the user with:

```
Handoff created! You can resume from this handoff in a new session with:

/resume_handoff thoughts/shared/handoffs/ARS-XXXX/YYYY-MM-DD_HH-MM-SS_ARS-XXXX_description.md
```

## Additional Notes
- **More information, not less** — this is a minimum; always include more if necessary
- **Be thorough and precise** — include both top-level objectives and lower-level details
- **Avoid excessive code snippets** — prefer `path/to/file.ext:line` references over large diffs
- **Never commit the thoughts/ directory** — handoffs stay local or are synced separately
