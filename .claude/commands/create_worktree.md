---
description: Create a git worktree for isolated feature development
---

# Create Worktree

You are tasked with setting up a git worktree for isolated implementation work.

## Process

### 1. Determine Required Information

Gather from the user or infer from context:
- Branch name (e.g., `ARS-14813/feat/add-anomaly-detail-card`)
- Path to implementation plan (e.g., `thoughts/shared/plans/2025-03-30-ARS-14813-anomaly-card.md`)
- Short name for the worktree directory (e.g., `ARS-14813`)

### 2. Confirm with User

```
Based on the input, I plan to create a worktree with:

Worktree path: ~/worktrees/reserved-ai/ARS-XXXX
Branch name: ARS-XXXX/feat/description
Plan file: thoughts/shared/plans/YYYY-MM-DD-ARS-XXXX-description.md

Command to run:
    git worktree add ~/worktrees/reserved-ai/ARS-XXXX -b ARS-XXXX/feat/description

Then open a new Claude Code session in:
    ~/worktrees/reserved-ai/ARS-XXXX

With prompt:
    /implement_plan thoughts/shared/plans/YYYY-MM-DD-ARS-XXXX-description.md

Shall I proceed?
```

### 3. Create the Worktree

```bash
# Create the worktrees parent directory if needed
mkdir -p ~/worktrees/reserved-ai

# Create the worktree on the new branch
git worktree add ~/worktrees/reserved-ai/ARS-XXXX -b BRANCH_NAME

# Verify
git worktree list
```

### 4. Set Up the Worktree

```bash
# Copy any local Claude settings if present
cp .claude/settings.local.json ~/worktrees/reserved-ai/ARS-XXXX/.claude/ 2>/dev/null || true

# Install frontend dependencies (they're not shared)
cd ~/worktrees/reserved-ai/ARS-XXXX/web && yarn install
```

### 5. Launch a New Session

Instruct the user to open a new Claude Code session in the worktree directory:

```
Worktree created at: ~/worktrees/reserved-ai/ARS-XXXX

To start implementing, open a new Claude Code session in that directory:

    claude ~/worktrees/reserved-ai/ARS-XXXX

Then run:
    /implement_plan thoughts/shared/plans/YYYY-MM-DD-ARS-XXXX-description.md
```

## Notes

- The `thoughts/` directory is accessible from any worktree (use relative paths)
- Always use `ONLY` the relative path for plan files (e.g., `thoughts/shared/plans/...` not the absolute path)
- To clean up a worktree after merging: `git worktree remove ~/worktrees/reserved-ai/ARS-XXXX`
- List all worktrees: `git worktree list`
