---
description: Create implementation plan for a Jira ticket ready for planning
---

# Plan Ticket

## PART I — IF A JIRA TICKET IS MENTIONED

0c. Save any provided ticket info to `thoughts/xifengjin/tickets/ARS-XXXX.md`
0d. Read the ticket and any comments/linked research to understand the implementation requirements

## PART I — IF NO TICKET IS MENTIONED

0a. Ask the user which Jira ticket needs a plan, or check the Jira board for tickets ready for planning
0b. Select the appropriate ticket
0c. Save ticket info to `thoughts/xifengjin/tickets/ARS-XXXX.md`
0d. Read the ticket and all linked documents to understand requirements

## PART II — NEXT STEPS

Think deeply.

1. Update the ticket status to "In Progress" (actively planning)
1a. Read `/create_plan` for guidance on writing implementation plans
1b. Check if a linked implementation plan already exists in `thoughts/shared/plans/`
1c. If the plan exists, respond with a link to it — you're done
1d. If no plan exists, proceed to create one following the instructions in `/create_plan`

Think deeply.

2. When the plan is complete:
2a. Save it to `thoughts/shared/plans/YYYY-MM-DD-ARS-XXXX-description.md`
2b. Add a comment to the Jira ticket linking to the plan document
2c. Update the ticket status to "In Review" (plan ready for review)

Think deeply, use TodoWrite to track your tasks.

## PART III — When You're Done

Print a summary message:

```
✅ Completed implementation plan for ARS-XXXX: [ticket title]

Plan saved to: thoughts/shared/plans/YYYY-MM-DD-ARS-XXXX-description.md

Implementation phases:
- Phase 1: [description]
- Phase 2: [description]
- Phase 3: [description if applicable]

Jira ticket: https://reserved.atlassian.net/browse/ARS-XXXX
```
