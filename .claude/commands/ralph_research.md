---
description: Research a Jira ticket needing investigation and save findings to thoughts/
---

# Research Ticket

## PART I — IF A JIRA TICKET IS MENTIONED

0c. Save any provided ticket info to `thoughts/xifengjin/tickets/ARS-XXXX.md`
0d. Read the ticket description to understand what research is needed

## PART I — IF NO TICKET IS MENTIONED

0a. Ask the user which Jira ticket needs research, or check the Jira board for tickets in "To Do" or "Backlog" status that need research
0b. Select the appropriate ticket
0c. Save the ticket info to `thoughts/xifengjin/tickets/ARS-XXXX.md`
0d. Read the ticket and any linked documents to understand what research is needed

## PART II — NEXT STEPS

Think deeply.

1. Update the ticket status to "In Progress" using available Jira tools
1a. Read any linked documents or existing research in `thoughts/shared/research/` for context
1b. If insufficient information to conduct research, add a comment asking for clarification

Think deeply about the research needs.

2. Conduct the research:
2a. Read `/research_codebase` guidance for effective codebase research
2b. If web research is needed, use the **web-search-researcher** agent
2c. Search the codebase for relevant implementations and patterns using the specialized agents
2d. Examine existing similar features or related code
2e. Identify technical constraints and opportunities
2f. **Be unbiased** — document all related files and how the systems work today, don't pre-design the solution
2g. Document findings in: `thoughts/shared/research/YYYY-MM-DD-ARS-XXXX-description.md`
   - Examples:
     - `2025-03-30-ARS-14813-anomaly-card-patterns.md`
     - `2025-03-30-cost-optimization-flow.md`

Think deeply about the findings.

3. Synthesize research into actionable insights:
3a. Summarize key findings and technical decisions
3b. Identify potential implementation approaches
3c. Note any risks or concerns discovered

4. Update the ticket:
4a. Add a comment to the Jira ticket summarizing research outcomes and linking the research doc
4b. Update the ticket status to reflect research is complete (e.g., "To Do" ready for planning)

Think deeply, use TodoWrite to track your tasks.

## PART III — When You're Done

Print a summary message:

```
✅ Completed research for ARS-XXXX: [ticket title]

Research saved to: thoughts/shared/research/YYYY-MM-DD-ARS-XXXX-description.md

Key findings:
- [Major finding 1]
- [Major finding 2]
- [Major finding 3]

Jira ticket: https://reserved.atlassian.net/browse/ARS-XXXX
```
