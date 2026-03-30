---
description: Implement a Jira ticket that is ready for development
model: sonnet
---

# Implement Ticket

## PART I — IF A TICKET IS MENTIONED

0c. Save any provided ticket info to `thoughts/xifengjin/tickets/ARS-XXXX.md`
0d. Read the ticket and all comments/linked docs to understand the implementation plan

## PART I — IF NO TICKET IS MENTIONED

0a. Check the Jira board for tickets in "To Do" status that are ready for development
0b. Select the highest priority ticket
0c. Save ticket info to `thoughts/xifengjin/tickets/ARS-XXXX.md`
0d. Read the ticket and all linked documents to understand the implementation plan

## PART II — NEXT STEPS

Think deeply.

1. Update the ticket status to "In Progress"
1a. Identify the linked implementation plan from the ticket (look for links to `thoughts/shared/plans/`)
1b. If no plan exists, move the ticket back to "To Do" and EXIT with explanation:
    "This ticket doesn't have an implementation plan. Please run /ralph_plan ARS-XXXX first."

Think deeply about the implementation.

2. Set up a branch for implementation:
```bash
git checkout web  # ensure you're on main branch
git pull
git checkout -b ARS-XXXX/feat/description
```

3. Implement the plan:
3a. Read `/implement_plan` for guidance
3b. Run: `/implement_plan thoughts/shared/plans/YYYY-MM-DD-ARS-XXXX-description.md`

4. When all tests pass and implementation is complete:
4a. Run `/commit` to create a commit
4b. Push the branch: `git push -u origin ARS-XXXX/feat/description`
4c. Run `/describe_pr` to create and fill a PR
4d. Add a comment to the Jira ticket with the PR link
4e. Update the ticket status to "In Review"

Think deeply, use TodoWrite to track your tasks. Work on ONE ticket at a time.

## PART III — When You're Done

```
✅ Implementation complete for ARS-XXXX: [ticket title]

Branch: ARS-XXXX/feat/description
PR: [PR URL]

Jira ticket: https://reserved.atlassian.net/browse/ARS-XXXX
Status updated to: In Review
```
