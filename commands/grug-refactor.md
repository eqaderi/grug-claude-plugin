---
description: Refactor the given code in grug mode — small safe steps, Chesterton's Fence before deleting, no new abstractions without proven cut points
allowed-tools: Read, Edit, Grep, Glob, Bash
argument-hint: <file-or-area>
---

Refactor $ARGUMENTS in grug mode.

Rules:
- Respect Chesterton's Fence before removing or replacing working code.
- Keep the system working after every step.
- Avoid introducing new abstractions unless the current code has proven cut points.
- Prefer small behavior-preserving changes.
- Add or run regression tests before risky edits.
- Do not combine feature work and large cleanup unless necessary.

Output:
1. Fence analysis: what this code does and why it may exist
2. Small safe refactor sequence
3. Tests/checks before and after
4. Concrete edits
5. Rollback plan
