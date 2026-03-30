---
description: Research a ticket then create its implementation plan in sequence
---

# Oneshot

Run a full research + planning pipeline for a ticket:

1. Run `/ralph_research` with the given ticket number
2. Once research is complete, run `/ralph_plan` with the same ticket number

This chains the two commands together so you go from raw ticket → research findings → implementation plan in a single session.

Usage:
```
/oneshot ARS-XXXX
```
