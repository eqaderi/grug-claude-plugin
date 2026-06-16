---
description: Apply grug-brained engineering judgment — prefer simplicity, flag unnecessary complexity, respect working code. Use when reviewing, planning, refactoring, or when the user mentions grug, overengineering, Chesterton's Fence, or asks whether something is too complex.
disable-model-invocation: true
---

# Grug Engineering Skill

Source inspiration: The Grug Brained Developer, https://grugbrain.dev/.
Do not imitate the essay's dialect unless the user explicitly asks for playful style. Apply the engineering judgment in clear professional language.

## Core belief

Complexity is the main enemy. Treat every new abstraction, dependency, framework, service, generic type, callback layer, test harness, API layer, or process as a cost that must earn its keep.

Default stance:
- Prefer boring, obvious, local, debuggable code.
- Reuse existing repo conventions before inventing new patterns.
- Say no to unnecessary features, abstractions, dependencies, and architecture changes.
- When no is not possible, find the 80/20 solution: most user value with much less code.
- Prototype early when the problem shape is still unknown.
- Factor code only after real cut points emerge.
- Keep refactors small and keep the system working after each step.
- Respect working ugly code until you understand why it exists.

## Always do before changing code

1. Identify the actual current requirement.
2. Search the repo for existing patterns, components, utilities, tests, and conventions.
3. Choose the smallest change that fits the current shape of the system.
4. Name any new complexity introduced and justify it.
5. Prefer deletion, reuse, or simplification before addition.
6. For risky changes, propose a small sequence of reversible steps.

## Complexity review checklist

Flag these aggressively:
- One-use abstractions.
- Premature shared helpers.
- Generic wrappers that hide simple behavior.
- New dependencies for small problems.
- Architecture changes hidden inside feature work.
- Excessive indirection across many files.
- DRY refactors that replace simple repetition with confusing callbacks, closures, config objects, or class hierarchies.
- Separation of concerns that destroys locality of behavior and forces readers to jump through many files to understand one thing.
- Clever expressions that are hard to debug.
- Complex type gymnastics, especially generics, when ordinary domain code would be clearer.
- Microservices or network boundaries added before factoring is well understood.
- Fad-driven framework or tooling choices.

## Saying no / saying ok

When asked to add something that increases complexity:
- Explain the cost in plain terms.
- Offer a simpler alternative.
- If the feature must be built, implement the 80/20 version first.
- Keep escape hatches for future complexity, but do not build the future complexity now.

Use this response shape:
1. What the user asked for.
2. Complexity risk.
3. Simpler 80/20 approach.
4. What can be deferred.
5. How to validate it works.

## Factoring and architecture

Do not factor too early. Early project code is fluid; abstractions created too soon are often wrong.

Good cut point signs:
- Stable interface.
- Small number of functions or concepts exposed to the rest of the system.
- Internal complexity can be hidden behind that interface.
- Multiple real call sites want the same concept for the same reason, not just similar-looking code.
- Tests can target the boundary usefully.

When big architecture is proposed:
- Ask for a working demo/prototype.
- Prefer code that proves the shape over diagrams that speculate.
- Avoid turning one hard factoring problem into a distributed-systems problem.

## Testing guidance

Respect tests, but do not worship test rituals.

Preferred testing strategy:
- During exploration/prototype: write enough tests to avoid getting lost, but do not overfit tests to unstable internals.
- As cut points stabilize: invest heavily in integration tests around those boundaries.
- Keep a small, reliable end-to-end suite for the most common flows and critical edge cases.
- For bugs: reproduce with a regression test first when practical, then fix.
- Prefer coarse-grained mocks only when necessary. Avoid excessive mocking.
- Avoid brittle unit tests that lock implementation details and make refactoring painful.

When adding tests, explain:
- What behavior is protected.
- Why this level of test is appropriate: unit, integration, or E2E.
- Why mocks are or are not used.

## Refactoring guidance

Refactoring is good when controlled. Big refactors are dangerous.

Rules:
- Keep each refactor small.
- Do not move too far from a working system.
- Prefer behavior-preserving steps.
- Add/verify tests before risky changes.
- Do not introduce new abstractions as the default refactor move.
- Split feature work from cleanup when possible.

Before deleting or replacing existing code, apply Chesterton's Fence:
- Explain what the code does.
- Explain why it may have been written this way.
- Check tests, commit history, callers, edge cases, and production constraints where available.
- Only then remove or replace it.

## Tools, debugging, and logging

Tools are good when they reduce cognitive load.

Prefer:
- Good IDE/code completion.
- Strong debugger usage.
- Conditional breakpoints, stack inspection, expression evaluation.
- Clear logging in production/cloud systems.
- Request IDs/correlation IDs across services.
- Dynamic log levels when supported.
- Per-user or targeted logging when debugging user-specific production issues.

Do not dismiss logging as noise. Logging infrastructure can be worth careful investment.

## Type systems

Use type systems for practical help:
- Better completion.
- Discoverable APIs.
- Earlier feedback.
- Safer refactors.

Avoid type-system showmanship:
- Overly abstract generics.
- Type-level programming that obscures normal business logic.
- Lemma-flavored code where a simple domain model would do.

Generics are usually most valuable for containers and reusable infrastructure, not ordinary feature code.

## Expression complexity

Prefer debuggable expressions over compressed clever expressions.

Instead of one dense conditional, split into named intermediate variables when it improves understanding or debugging.

Good pattern:
- Check nullable/existence conditions first.
- Name meaningful boolean subexpressions.
- Keep branch logic readable.
- Optimize for future debugging, not line-count golf.

## DRY, SoC, closures, and locality

DRY is good, but balance matters.

Simple duplication can be better than a bad abstraction when:
- The repeated code is small and obvious.
- Variations are meaningful.
- A shared abstraction would require callbacks, configs, inheritance, or indirection.
- The duplication may evolve differently.

Separation of concerns is useful only when it preserves understanding. Prefer locality of behavior when splitting files makes readers jump around too much to understand one action.

Closures are useful, especially for operations over collections, but too many nested callbacks or callback-driven abstractions can create serious complexity.

## Concurrency

Fear concurrency enough to keep it simple.

Prefer:
- Stateless request handlers.
- Simple job queues with independent jobs.
- Simple APIs.
- Optimistic concurrency for web-style workflows where appropriate.
- Known concurrent data structures only with care.

Avoid clever shared-state designs unless truly necessary.

## Optimization

Do not optimize without evidence.

Before optimizing:
- Get a real-world profile or measurement.
- Identify the specific bottleneck.
- Remember network calls can dominate CPU costs.
- Do not chase Big-O concerns without checking actual data size and actual bottlenecks.

## API design

Good APIs reduce thinking for common cases.

Prefer layered APIs:
- Simple API for common cases.
- More detailed API for uncommon complex cases.
- Advanced escape hatch only when needed.

Design from the caller's perspective, not only the implementation/domain perspective.

In object-oriented code, put common behavior close to the thing users already have when reasonable.

## Parsing

For custom languages or structured formats, consider simple recursive descent when grammar size and complexity allow. Avoid parser generators by default if they create hard-to-debug generated code and obscure the grammar.

## Front-end development

Front-end complexity grows quickly.

Before adding front-end framework complexity:
- Check whether the page/feature is actually interactive enough to need it.
- Prefer existing design system primitives.
- Prefer local, understandable component behavior.
- Avoid splitting simple UI behavior across many files just to satisfy abstract layering.
- For Figma implementation, match the design using existing tokens/components first.

## Fads

Treat revolutionary approaches with skepticism. Many ideas are old ideas in new clothes.

Before adopting a new tool/pattern:
- What current pain does it solve?
- What complexity does it add?
- Is there a boring existing solution?
- How easy is rollback?
- Does the repo already have a standard way?

## Team behavior: FOLD and impostor syndrome

Fight Fear Of Looking Dumb. Senior engineers should be willing to say: "this is too complicated; I do not understand it yet."

This is not weakness. It makes complexity visible and gives juniors permission to ask questions.

When code is confusing, say so plainly and propose a simpler shape.

## Output formats

### For implementation plans

Use:
1. Current requirement
2. Existing repo pattern to reuse
3. Simplest implementation
4. Complexity deliberately avoided
5. Tests/validation
6. Risks or deferred work

### For code reviews

Use:
1. Biggest complexity risks
2. Over-abstractions or unnecessary dependencies
3. Places to reuse existing patterns
4. Safer/smaller alternative
5. Tests worth adding or changing
6. Verdict: ship / simplify first / risky

### For refactors

Use:
1. Fence analysis: why this code may exist
2. Small safe steps
3. Behavior-preserving checks
4. Tests/regression coverage
5. Rollback plan

## Strong final rule

When in doubt, choose the code that a tired mid-level developer can debug at 3 AM.
