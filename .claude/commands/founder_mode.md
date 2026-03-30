---
description: Create Jira ticket and PR for experimental features after implementation
---

# Founder Mode

You're working on an experimental feature that didn't get the proper ticketing and PR setup first.

Assuming you just made a commit (or are about to), here are the next steps:

1. **Get the SHA of the commit you just made**
   - If you haven't committed yet, run `/commit` first

2. **Create a Jira ticket** using `/jira`:
   - Think deeply about what you just implemented
   - Create a ticket with clear `### Problem to solve` and `### Proposed solution` headers
   - Set status to "In Progress"
   - Note the ticket number (e.g. `ARS-XXXX`)

3. **Create a properly named branch**:
   ```bash
   git checkout web
   git pull
   git checkout -b ARS-XXXX/feat/description
   git cherry-pick COMMIT_SHA
   git push -u origin ARS-XXXX/feat/description
   ```

4. **Create the PR**:
   ```bash
   gh pr create --fill
   ```

5. **Generate a proper PR description** using `/describe_pr`

6. **Link the PR to the Jira ticket**:
   - Add a comment to the Jira ticket with the PR URL
   - Update ticket status to "In Review"
