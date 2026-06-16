# Global Grug Engineering Instructions

Use these instructions for software tasks when simplicity, maintainability, implementation planning, review, refactoring, testing, or architecture judgment matters.

Source inspiration: The Grug Brained Developer, https://grugbrain.dev/.
Apply the ideas in normal professional language unless explicitly asked for caveman style.

## Default engineering bias

Complexity is the main enemy. Prefer simple, boring, debuggable code that follows existing repo conventions.

Before implementing:
- Identify the actual current requirement.
- Inspect existing repo patterns before inventing new ones.
- Reuse components, tokens, utilities, hooks, services, tests, and conventions when possible.
- Choose the smallest change that works.
- Name any new complexity and justify why it is necessary.
- Avoid speculative future-proofing.

## Complexity rules

Say no or propose a simpler 80/20 alternative when a request introduces unnecessary:
- abstraction
- dependency
- framework
- service boundary
- generic type machinery
- callback/config indirection
- architecture change
- process ceremony

Prefer prototypes when the problem shape is unknown. Factor code after real cut points emerge, not before.

## Refactoring

Keep refactors small. Keep the system working after every step.

Before deleting or replacing working code, apply Chesterton's Fence:
- Understand what the code does.
- Understand why it may exist.
- Check tests/callers/history where practical.
- Only then remove or replace it.

## Testing

Use tests pragmatically:
- Integration tests around stable cut points are usually the sweet spot.
- Keep a small reliable E2E suite for critical flows.
- Use unit tests where they help, but avoid brittle tests that freeze implementation details.
- For bugs, reproduce with a regression test first when practical.
- Avoid excessive mocking; prefer coarse mocks only when necessary.

## Code style

Optimize for debugging and reading:
- Split dense expressions into named intermediate variables when helpful.
- Prefer locality of behavior over file-splitting that forces readers to jump around.
- Accept small obvious duplication when a DRY abstraction would be more confusing.
- Avoid clever type/generic code in ordinary feature logic.

## Tooling, logs, performance

Use tools to reduce cognitive load:
- Debuggers are valuable.
- Logging matters, especially in production/cloud systems.
- Include request/correlation IDs across service boundaries when relevant.
- Optimize only with real measurements/profiles.
- Remember network costs often dominate CPU costs.

## Team behavior

It is good to say: "this is too complicated; I do not understand it yet." Do not hide confusion. Make complexity visible and simplify it.
