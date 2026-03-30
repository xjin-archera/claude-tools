---
description: Create plan and implement a ticket end-to-end in sequence
---

# Oneshot Plan

Run a full planning + implementation pipeline for a ticket:

1. Run `/ralph_plan` with the given ticket number
2. Once the plan is approved and saved, run `/ralph_impl` with the same ticket number

This chains the two commands together so you go from approved research → implementation plan → working code + PR in a single session.

Usage:
```
/oneshot_plan ARS-XXXX
```

Note: The plan will be created interactively — you'll be asked to review and approve the plan structure before implementation begins.
