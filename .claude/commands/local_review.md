---
description: Set up a worktree for reviewing a colleague's branch
---

# Local Review

You are tasked with setting up a local review environment for a colleague's branch.

## Process

When invoked with a parameter like `gh_username:branchName`:

1. **Parse the input**:
   - Extract GitHub username and branch name from `username:branchname`
   - If no parameter provided, ask: "Please provide the branch in the format `gh_username:branchName`"

2. **Extract ticket information**:
   - Look for ticket numbers in the branch name (e.g., `ars-14813`, `ARS-14813`)
   - Use this to create a short worktree directory name
   - If no ticket found, use a sanitized version of the branch name

3. **Set up the remote and worktree**:
   ```bash
   # Check if remote already exists
   git remote -v | grep USERNAME

   # If not, add it
   git remote add USERNAME git@github.com:USERNAME/reserved-ai.git

   # Fetch from the remote
   git fetch USERNAME

   # Create the worktree
   git worktree add -b BRANCHNAME ~/worktrees/reserved-ai/SHORT_NAME USERNAME/BRANCHNAME
   ```

4. **Set up the worktree**:
   ```bash
   # Copy local Claude settings if present
   cp .claude/settings.local.json ~/worktrees/reserved-ai/SHORT_NAME/.claude/ 2>/dev/null || true

   # Install frontend dependencies
   cd ~/worktrees/reserved-ai/SHORT_NAME/web && yarn install
   ```

5. **Inform the user**:
   ```
   Review environment ready at: ~/worktrees/reserved-ai/SHORT_NAME

   Open a new Claude Code session there to review:
       claude ~/worktrees/reserved-ai/SHORT_NAME

   Or just navigate to the directory to review manually.

   When done, clean up with:
       git worktree remove ~/worktrees/reserved-ai/SHORT_NAME
       git remote remove USERNAME  # if you don't need the remote anymore
   ```

## Error Handling

- If worktree already exists: inform the user to remove it first with `git worktree remove path`
- If remote fetch fails: check if the username/repo combination is correct
- If setup fails: report the error but note the worktree was still created

## Example Usage

```
/local_review teammate:ARS-14813/feat/add-anomaly-detail-card
```

This will:
- Add 'teammate' as a git remote
- Create worktree at `~/worktrees/reserved-ai/ARS-14813`
- Set up the environment for review
