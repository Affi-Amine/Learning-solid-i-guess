# Acceptance Tests

**Origin**: Extreme Programming (XP); formalized with BDD by Dan North (2003)

## What It Is

An **acceptance test** verifies that a feature works **from the customer's perspective**. It's specified by the customer (or domain expert) using BDD-style scenarios, then automated by developers.

## The Format (BDD)

```
Given [some context]
When [some action]
Then [some expected outcome]
```

Example:
```
Given I have an account
When I try to login with valid credentials
Then I should be redirected to the dashboard
```

## Why It Matters

- **Customer specifies done** — not the developer. The test IS the specification.
- **Prevents the #1 bug source** — misunderstood requirements
- **Living documentation** — tests describe what the system does, and they run
- **Regression safety** — features can't break silently

## Double-Loop TDD

Acceptance tests drive **outer loop** TDD. Unit tests drive the **inner loop**:

1. Write a failing acceptance test (outer loop, red)
2. Write failing unit tests for the objects needed (inner loop, red)
3. Make unit tests pass (inner loop, green)
4. Refactor (inner loop, refactor)
5. Repeat inner loop until acceptance test passes (outer loop, green)

The outer loop prevents regressions. The inner loop measures progress.

## Acceptance Tests vs. Other Tests

| Type | Tests What | Written By | Speed |
|---|---|---|---|
| **Acceptance** | Feature works end-to-end for customer | Customer + dev | Slow |
| **Integration** | Components work together | Developer | Medium |
| **Unit** | Single object/function works | Developer | Fast |

## Related

- [TDD](./tdd.md) — acceptance tests are the outer loop
- [Domain Events](./domain-events.md) — events trigger features tested by acceptance tests
- [Feature-Driven Structure](./feature-driven-structure.md) — acceptance tests live in feature folders
