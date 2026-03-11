# Test-Driven Development (TDD)

**Origin**: Kent Beck, rediscovered from early programming practices

## The Cycle: Red-Green-Refactor

```
🔴 RED    → Write a failing test (define what you want)
🟢 GREEN  → Write the minimum code to make it pass
🔵 REFACTOR → Clean up without changing behavior
```

Repeat. Every piece of production code exists because a test demanded it.

## The Three Laws of TDD (Robert C. Martin)

1. You may not write production code unless you have a failing test
2. You may not write more of a test than is sufficient to fail
3. You may not write more production code than is sufficient to pass the test

## Why TDD Matters

- **Confidence**: Tests prove your code works
- **Design feedback**: Hard to test = bad design (TDD forces you to notice)
- **Emergent design**: Structure emerges from small, tested increments
- **Safety net**: Refactor without fear of breaking things
- **Documentation**: Tests describe what the code *should* do

## TDD and Simple Design

TDD is the **engine** that drives Simple Design:

| Simple Design Element | TDD Connection |
|---|---|
| Runs all tests | You wrote them first |
| No duplication | Refactor step catches it |
| Maximizes clarity | Refactor step improves it |
| Fewer elements | You only wrote what tests required |

## Common Misconceptions

- ❌ "TDD is about testing" → It's about **design**. Tests are a side effect.
- ❌ "TDD is slower" → It's slower *at first*, faster over the project lifetime.
- ❌ "Write all tests first" → No. One test at a time, tiny cycles.
- ❌ "100% coverage is the goal" → Meaningful tests > coverage numbers.

## Related

- [Simple Design](./simple-design.md)
- [Emergent Design](./emergent-design.md)
- [Code Smells](./code-smells.md) — what you look for in the refactor step
