---
description: Manage Jira tickets - create, update, comment, and follow workflow patterns
---

# Jira - Ticket Management

You are tasked with managing Jira tickets, including creating tickets, updating existing ones, adding comments, and following the team's workflow.

## Initial Setup

First, verify that Jira MCP tools are available by checking if any `mcp__jira__` tools exist.
If not, check for a `jira` CLI tool: `which jira`.
If neither is available, inform the user:
```
I need access to Jira tools. Please ensure either the Jira MCP server is configured
or the Jira CLI is installed and authenticated.
```

## Ticket Format

- **Project key**: `ARS` (e.g., `ARS-14813`)
- **Branch naming**: `ARS-{number}/[feat|fix|infra|chore|doc|dep]/description`
- **Jira base URL**: `https://reserved.atlassian.net/browse/ARS-XXXX`

## Workflow States

The team follows this progression:
1. **Backlog** → New tickets start here
2. **To Do** → Triaged and ready to be picked up
3. **In Progress** → Active development
4. **In Review** → PR submitted, awaiting code review
5. **Done** → Completed and merged

## Action-Specific Instructions

### 1. Creating Tickets

1. **Gather information**:
   - If given a thoughts document, read it fully
   - If given a topic, ask for more context

2. **Draft the ticket**:
   Present a draft before creating:
   ```
   ## Draft Jira Ticket

   **Summary**: [Clear, action-oriented title]

   **Description**:

   ### Problem to solve
   [2-3 sentence description of the problem from a user/developer perspective]

   ### Proposed solution
   [High-level approach]

   ### Technical details (if applicable)
   - [Key implementation notes]
   - [Relevant file:line references]

   ### References
   - Related code: [file:line]
   - Research doc: [path if applicable]
   ```

3. **Get user confirmation** on title, description, priority, and type

4. **Create the ticket** using available Jira tools/CLI

5. **Post-creation**: Show the ticket URL and ask if user wants to add more details

### 2. Adding Comments to Existing Tickets

1. **Determine which ticket** from context or ask
2. **Format comments for clarity**:
   - Keep comments concise (~10 lines) unless more detail is needed
   - Focus on key insights, not mechanical summaries
   - Include relevant file references with backticks
3. **Comment structure**:
   ```
   Implemented [feature/fix] for [reason].

   Key insight: [The most important thing to know]

   Files updated:
   - `server/src/path/to/file.py:45` — [what changed]
   - `web/src/path/to/component.tsx:12` — [what changed]
   ```

### 3. Searching for Tickets

Gather search criteria (text query, status, assignee) and search using available tools.

Present results grouped by status with ticket ID, title, status, and link.

### 4. Updating Ticket Status

When moving tickets:
1. Fetch current status
2. Suggest next status based on workflow
3. Update and optionally add a brief comment explaining the change

### 5. Linking to PRs

When a PR is created for a ticket:
1. Add a comment to the Jira ticket with the PR link
2. Move the ticket to "In Review"
3. Format: `PR: {gh pr view --json url -q .url}`

## Ticket Quality Guidelines

- All tickets should have a clear "problem to solve" from a user/developer perspective
- If the user only gives implementation details, ask: "What problem are you trying to solve?"
- Keep titles concise and action-oriented (imperative mood)
- Include code references as: `path/to/file.ext:linenum`
- Focus on "what" and "why"; include "how" only if well-defined

## Comment Quality Guidelines

Focus on:
- **Key insights**: The "aha" moment or critical understanding
- **Decisions and tradeoffs**: What approach was chosen and why
- **Blockers resolved**: What was preventing progress and how it was addressed
- **State changes**: What's different now and what it means for next steps

Avoid:
- Mechanical lists of changes without context
- Restating what's obvious from the code diff
- Generic summaries that don't add value
