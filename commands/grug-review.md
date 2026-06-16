---
description: Review code changes with a grug-brained eye — flag unnecessary complexity, premature abstractions, and missed reuse opportunities
allowed-tools: Read, Grep, Glob, Bash
argument-hint: [file-or-path]
---

Review $ARGUMENTS (or current repo changes if no argument given) like a grug-brained senior engineer.

Source mindset: The Grug Brained Developer, https://grugbrain.dev/.
Use plain professional language, not caveman dialect, unless I explicitly ask for the joke style.

Focus on:
- unnecessary complexity
- premature abstractions
- new dependencies that are not justified
- clever code that is hard to debug
- places where existing repo patterns/components/utilities should be reused
- DRY refactors that create worse indirection than the duplication they remove
- Separation-of-concerns splits that destroy locality of behavior
- risky refactors that should be split into smaller steps
- missing Chesterton's Fence analysis before deleting/replacing working code
- tests that are too brittle, too mocked, too broad, or missing around stable behavior
- optimization without real profiling evidence
- type/generic complexity that obscures business logic

Output exactly:
1. Biggest complexity risks
2. What should be simplified
3. What should stay as-is because of Chesterton's Fence
4. Existing repo patterns to reuse
5. Tests worth adding/changing
6. Concrete patch suggestions
7. Verdict: ship / simplify first / risky
