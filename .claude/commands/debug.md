---
description: Debug issues by investigating logs, server state, and git history
---

# Debug

You are tasked with helping debug issues during manual testing or implementation. Investigate problems by examining logs, server state, and git history without editing files.

## Initial Response

When invoked WITH context (plan/ticket file):
```
I'll help debug issues with [file name]. What specific problem are you encountering?
- What were you trying to test/implement?
- What went wrong?
- Any error messages or stack traces?
```

When invoked WITHOUT parameters:
```
I'll help debug your current issue. Please describe what's going wrong:
- What are you working on?
- What specific problem occurred?
- When did it last work?
```

## Environment Information

**Local Server** (Flask API on port 5000):
- Check if running: `lsof -i :5000 | grep LISTEN`
- Logs: Check the terminal running `cd server && ./rcli api start`
- Flask debug output is printed to stdout

**Local Frontend** (Vite dev server, usually port 5173):
- Check if running: `lsof -i :5173 | grep LISTEN`
- Logs: Check the terminal running `cd web && make start`

**Database (PostgreSQL)**:
- Connect: `cd server && uv run python -c "from reservedai.db.session import get_session; ..."`
- Or use the Django-style shell: check if `./rcli shell` exists
- Migrations status: `cd server && uv run alembic current`
- Pending migrations: `cd server && uv run alembic heads`

**Redis (optional caching)**:
- Check if running: `redis-cli ping`

**Git State**:
- Current branch, recent commits, uncommitted changes

## Process Steps

### Step 1: Understand the Problem

1. **Read any provided context** (plan or ticket file)
2. **Quick state check**:
   ```bash
   git branch --show-current
   git log --oneline -5
   git status
   ```

### Step 2: Investigate the Issue

Spawn parallel investigation tasks:

**Task 1 — Check Server Logs:**
- Look at the server terminal output for errors/tracebacks
- Run the failing request and observe the Flask error output
- Check for 5xx error responses with stack traces
- Look for `logger.error()` / `logger.exception()` output

**Task 2 — Check Git/File State:**
- `git status` — uncommitted changes
- `git log --oneline -10` — recent commits
- `git diff` — what's changed
- Verify expected files exist at expected paths

**Task 3 — Check Database State (if relevant):**
- `cd server && uv run alembic current` — migration state
- `cd server && uv run python -c "..."` — query DB state inline

### Step 3: Present Findings

```markdown
## Debug Report

### What's Wrong
[Clear statement of the issue based on evidence]

### Evidence Found

**From Server Logs:**
- [Error with traceback or relevant log line]

**From Database:**
- [Migration state or relevant query result]

**From Git/Files:**
- [Recent change that might be related]

### Root Cause
[Most likely explanation based on evidence]

### Next Steps

1. **Try This First:**
   ```bash
   [Specific command or action]
   ```

2. **If That Doesn't Work:**
   - Restart server: `cd server && ./rcli api start`
   - Check browser console (F12) for frontend errors
   - Run relevant test: `cd server && uv run pytest -s path/to/test.py`

### Can't Access?
Some things are outside reach:
- Browser console errors (F12 in browser)
- Docker container logs (if running in Docker)
- External service responses (AWS, Snowflake, etc.)
```

## Quick Reference

**Check server is running:**
```bash
lsof -i :5000 | grep LISTEN
```

**Check frontend is running:**
```bash
lsof -i :5173 | grep LISTEN
```

**Run a single backend test:**
```bash
cd server && uv run pytest -s path/to/test_file.py
cd server && uv run pytest -s -k "test_name_here"
```

**Check migration state:**
```bash
cd server && uv run alembic current
cd server && uv run alembic history --verbose
```

**Git state:**
```bash
git status
git log --oneline -10
git diff
```

## Important Notes

- **Focus on manual testing scenarios** — this is for debugging during implementation
- **No file editing** — pure investigation only
- **Read files completely** when context files are provided
- **Guide back to user** for things outside reach (browser console, external APIs)
