# Code Smells

**Origin**: Martin Fowler & Kent Beck, "Refactoring" (1999)

## What They Are

A **code smell** is a surface-level indication that something *might* be wrong with the design. Not a bug — the code works. But something about it suggests a deeper problem.

Smells are **heuristics**, not rules. They point you toward potential problems to investigate.

## Common Smells


| Smell                   | Sign                                               | Likely Problem                 |
| ----------------------- | -------------------------------------------------- | ------------------------------ |
| **Duplication**         | Same logic in multiple places                      | Missing abstraction            |
| **Long Method**         | Method does too many things                        | Low cohesion                   |
| **Large Class**         | Class has too many responsibilities                | Violates Single Responsibility |
| **Feature Envy**        | Method uses another class's data more than its own | Logic in the wrong place       |
| **Primitive Obsession** | Using strings/ints where a domain type fits        | Missing domain model           |
| **Shotgun Surgery**     | One change requires edits in many places           | Tight coupling                 |
| **Divergent Change**    | One class changes for many different reasons       | Low cohesion                   |
| **Dead Code**           | Code that's never executed                         | Unnecessary elements           |
| **Comments**            | Excessive comments explaining *what* code does     | Code isn't self-explanatory    |


## When to Act

In TDD's refactor step: after tests pass, scan for smells. If you find one, refactor. If you don't, move on.

**Don't**: preemptively refactor code that doesn't smell yet.
**Do**: address smells as you encounter them.

## The Relationship to Simple Design

Code smells are violations of Simple Design elements:

- Duplication → violates "no duplication"
- Unclear naming → violates "maximizes clarity"
- Dead code → violates "fewer elements"

## Related

- [Simple Design](./simple-design.md)
- [TDD](./tdd.md) — smells are caught during the refactor step
- [Accidental vs Essential Complexity](./accidental-vs-essential-complexity.md) — smells are often accidental complexity

