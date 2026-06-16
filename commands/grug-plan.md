---
description: Plan a task the grug way — smallest change that works, reuse existing patterns, avoid speculative complexity
allowed-tools: Read, Grep, Glob, Bash
argument-hint: <task description>
---

Plan this task: $ARGUMENTS

Use grug engineering principles from https://grugbrain.dev/.

Do not over-engineer. Before proposing code, inspect the repo for existing patterns and choose the smallest implementation that satisfies the current requirement.

Output:
1. Current requirement in one sentence
2. Existing repo patterns/components/utilities to reuse
3. Simplest working approach
4. Complexity deliberately avoided
5. What to defer
6. Tests/validation
7. Risks
