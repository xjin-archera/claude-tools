---
description: Create git commits for session changes autonomously with clear, atomic messages
---

# Commit Changes (CI / Autonomous Mode)

You are tasked with creating git commits for the changes made during this session. Proceed autonomously without asking for confirmation.

## Process:

1. **Think about what changed:**
   - Review the conversation history and understand what was accomplished
   - Run `git status` to see current changes
   - Run `git diff` to understand the modifications
   - Consider whether changes should be one commit or multiple logical commits

2. **Plan your commit(s):**
   - Identify which files belong together
   - Draft clear, descriptive commit messages
   - Use imperative mood in commit messages
   - Focus on why the changes were made, not just what
   - Include the Jira ticket ID (e.g. `ARS-14813`) in commit messages when working on a ticket

3. **Execute:**
   - Use `git add` with specific files (never use `-A` or `.`)
   - Never commit the `thoughts/` directory or anything inside it
   - Never commit dummy files, test scripts, or other files which were created incidentally
   - Create commits with your planned messages

## Remember:
- You have the full context of what was done in this session
- Group related changes together
- Keep commits focused and atomic when possible
- **IMPORTANT**: Never stop and ask for feedback from the user
- Main branch is `web` (not `main` or `master`)
