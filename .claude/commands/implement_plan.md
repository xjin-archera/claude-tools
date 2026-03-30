---
description: Implement technical plans from thoughts/shared/plans with verification
---

# Implement Plan

You are tasked with implementing an approved technical plan. These plans contain phases with specific changes and success criteria.

## Getting Started

When given a plan path:
- Read the plan completely and check for any existing checkmarks (`- [x]`)
- Read all files mentioned in the plan
- **Read files fully** — never use limit/offset parameters, you need complete context
- Think deeply about how the pieces fit together
- Create a todo list to track your progress
- Start implementing

If no plan path provided, ask for one.

## Implementation Philosophy

Plans are carefully designed, but reality can be messy. Your job is to:
- Follow the plan's intent while adapting to what you find
- Implement each phase fully before moving to the next
- Verify your work makes sense in the broader codebase context
- Update checkboxes in the plan as you complete sections

When things don't match the plan exactly, think about why and communicate clearly:
```
Issue in Phase [N]:
Expected: [what the plan says]
Found: [actual situation]
Why this matters: [explanation]

How should I proceed?
```

## Verification Approach

After implementing a phase, run the success criteria checks:

**Backend changes:**
```bash
cd server && make lint
cd server && uv run pytest -s path/to/relevant_test.py
```

**Frontend changes:**
```bash
cd web && make lint
cd web && make validate-types
cd web && make test
```

Fix any issues before proceeding. Update your progress in both the plan and your todos.

**Pause for human verification**: After all automated checks pass, inform the human:
```
Phase [N] Complete - Ready for Manual Verification

Automated verification passed:
- [List automated checks that passed]

Please perform the manual verification steps listed in the plan:
- [List manual verification items]

Let me know when manual testing is complete so I can proceed to Phase [N+1].
```

If instructed to execute multiple phases consecutively, skip the pause until the last phase.

Do not check off manual testing items until confirmed by the user.

## If You Get Stuck

- Make sure you've read and understood all relevant code
- Consider if the codebase has evolved since the plan was written
- Present the mismatch clearly and ask for guidance

## Resuming Work

If the plan has existing checkmarks:
- Trust that completed work is done
- Pick up from the first unchecked item
- Verify previous work only if something seems off

## Code Conventions

When implementing, follow these codebase patterns:

**Backend (server/):**
- SQLAlchemy 2.0: `session.scalars(select(Model)).all()`
- Never commit inside a function that receives a `Session`
- Raise `APIException` (never `abort()`), `DomainError`, `ProviderError`
- Prefer `selectinload`/`joinedload` to avoid N+1 queries
- Type hints on all function signatures

**Frontend (web/):**
- Destructure imports: `import { foo } from 'bar'`
- Add imports and usages in the same edit
- API types come from generated OpenAPI schema

Remember: You're implementing a solution, not just checking boxes. Keep the end goal in mind.
