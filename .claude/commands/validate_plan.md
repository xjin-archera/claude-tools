---
description: Validate implementation against plan, verify success criteria, identify issues
---

# Validate Plan

You are tasked with validating that an implementation plan was correctly executed, verifying all success criteria and identifying any deviations or issues.

## Initial Setup

When invoked:
1. **Determine context** — Are you in an existing conversation or starting fresh?
   - Existing: Review what was implemented in this session
   - Fresh: Discover what was done through git and codebase analysis

2. **Locate the plan**:
   - If plan path provided, use it
   - Otherwise, search recent commits for plan references or ask user

3. **Gather implementation evidence**:
   ```bash
   git log --oneline -n 20
   git diff HEAD~N..HEAD  # where N covers implementation commits
   ```

4. **Run comprehensive checks**:
   ```bash
   # Backend
   cd server && make lint
   cd server && uv run pytest -s

   # Frontend
   cd web && make lint
   cd web && make validate-types
   cd web && make test
   ```

## Validation Process

### Step 1: Context Discovery

1. **Read the implementation plan** completely
2. **Identify what should have changed**:
   - All files that should be modified
   - All success criteria (automated and manual)
   - Key functionality to verify

3. **Spawn parallel research tasks** to discover implementation:
   - Verify database/migration changes match plan
   - Verify code changes match plan specifications
   - Verify test coverage was added as specified

### Step 2: Systematic Validation

For each phase in the plan:

1. **Check completion status** — Look for checkmarks (`- [x]`), verify actual code matches
2. **Run automated verification** — Execute each command, document pass/fail
3. **Assess manual criteria** — List what needs manual testing with clear steps
4. **Think about edge cases** — Error conditions, missing validations, regressions

### Step 3: Generate Validation Report

```markdown
## Validation Report: [Plan Name]

### Implementation Status
✓ Phase 1: [Name] - Fully implemented
✓ Phase 2: [Name] - Fully implemented
⚠️ Phase 3: [Name] - Partially implemented (see issues)

### Automated Verification Results
✓ Backend lint: `cd server && make lint`
✓ Backend tests: `cd server && uv run pytest -s`
✓ Frontend lint: `cd web && make lint`
✓ TypeScript types: `cd web && make validate-types`
✗ Frontend tests: `cd web && make test` — 2 failing tests (see below)

### Code Review Findings

#### Matches Plan:
- [Specific thing that matches]
- [Another match]

#### Deviations from Plan:
- [Deviation at file:line] — why and whether it's acceptable

#### Potential Issues:
- [Issue found during review]

### Manual Testing Required:
1. UI functionality:
   - [ ] Verify [feature] appears correctly
   - [ ] Test error states with invalid input

2. Integration:
   - [ ] Confirm works with existing [component]

### Summary
[Overall assessment — ready to merge, needs fixes, etc.]
```

## Working with Existing Context

If you were part of the implementation:
- Review the conversation history
- Check your todo list for what was completed
- Focus validation on work done in this session
- Be honest about any shortcuts or incomplete items

## Validation Checklist

Always verify:
- [ ] All phases marked complete are actually done
- [ ] Backend lint passes
- [ ] Backend tests pass
- [ ] Frontend lint passes
- [ ] TypeScript types are valid
- [ ] Frontend tests pass
- [ ] Code follows existing codebase patterns
- [ ] No regressions introduced
- [ ] Error handling is robust
- [ ] Alembic migration present if schema changed
