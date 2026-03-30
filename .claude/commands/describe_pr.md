---
description: Generate comprehensive PR descriptions and update the PR on GitHub
---

# Generate PR Description

You are tasked with generating a comprehensive pull request description.

## PR Description Template

Use this template for all PRs:

```md
## What problem(s) was I solving?

## What user-facing changes did I ship?

## How I implemented it

## How to verify it

### Automated Checks
- [ ] Backend lint passes: `cd server && make lint`
- [ ] Frontend lint passes: `cd web && make lint`
- [ ] TypeScript types valid: `cd web && make validate-types`
- [ ] Backend tests pass: `cd server && uv run pytest -s`
- [ ] Frontend tests pass: `cd web && make test`

### Manual Testing

## Jira ticket
[ARS-XXXX](https://reserved.atlassian.net/browse/ARS-XXXX)

## Description for the changelog
```

## Steps to follow:

1. **Identify the PR:**
   - Check if the current branch has an associated PR: `gh pr view --json url,number,title,state 2>/dev/null`
   - If no PR exists, list open PRs: `gh pr list --limit 10 --json number,title,headRefName,author`
   - Ask the user which PR they want to describe if ambiguous

2. **Check for existing description:**
   - Check if `thoughts/shared/prs/{number}_description.md` already exists
   - If it exists, read it and inform the user you'll be updating it

3. **Gather comprehensive PR information:**
   - Get the full PR diff: `gh pr diff {number}`
   - Get commit history: `gh pr view {number} --json commits`
   - Review the base branch: `gh pr view {number} --json baseRefName`
   - Get PR metadata: `gh pr view {number} --json url,title,number,state`

4. **Analyze the changes thoroughly:**
   - Read through the entire diff carefully
   - For context, read any files referenced but not shown in the diff
   - Understand the purpose and impact of each change
   - Identify user-facing changes vs internal implementation details
   - Look for breaking changes or migration requirements

5. **Handle verification requirements:**
   - Run each automated check listed in the template
   - If it passes, mark the checkbox: `- [x]`
   - If it fails, keep it unchecked and note what failed: `- [ ]` with explanation
   - If it requires manual testing (UI interactions), leave unchecked and note for user

6. **Generate the description:**
   - Fill out each section thoroughly
   - Be specific about problems solved and changes made
   - Focus on user impact where relevant
   - Include technical details in appropriate sections
   - Extract the Jira ticket ID from the branch name (e.g. `ARS-14813/feat/...` → `ARS-14813`)

7. **Save the description:**
   - Write the completed description to `thoughts/shared/prs/{number}_description.md` if thoughts/ exists
   - Show the user the generated description

8. **Update the PR:**
   - Update the PR: `gh pr edit {number} --body "$(cat thoughts/shared/prs/{number}_description.md)"`
   - Or pipe directly if not saving to thoughts/
   - Confirm the update was successful
   - Remind the user of any unchecked manual testing steps

## Important notes:
- Be thorough but concise — descriptions should be scannable
- Focus on the "why" as much as the "what"
- Include any breaking changes or migration notes prominently
- If the PR touches both `server/` and `web/`, organize the description by layer
- Always attempt to run verification commands when possible
