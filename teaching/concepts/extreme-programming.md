# Extreme Programming (XP)

**Origin**: Kent Beck, late 1990s

## What It Is

A set of software development practices designed to improve software quality and responsiveness to changing requirements. XP takes good practices and pushes them to their "extreme" — if code review is good, do it all the time (pair programming). If testing is good, test constantly (TDD).

## Core Values

1. **Communication** — everyone talks, no silos
2. **Simplicity** — build only what's needed now
3. **Feedback** — fast loops at every level
4. **Courage** — make hard decisions, refactor ruthlessly
5. **Respect** — for teammates, for the codebase

## Key Practices Relevant to Clean Code


| Practice                      | What It Means                                              |
| ----------------------------- | ---------------------------------------------------------- |
| **Shared Understanding**      | Everyone knows how the codebase works                      |
| **Coding Standards**          | Agreed-upon rules for consistency                          |
| **Collective Code Ownership** | Anyone can change any code                                 |
| **Simple Design**             | 4 elements: tests, no duplication, clarity, fewer elements |
| **System Metaphor**           | Use domain language in code (→ DDD)                        |
| **TDD**                       | Write tests first, always                                  |
| **Pair Programming**          | Two devs, one keyboard — continuous review                 |
| **Continuous Integration**    | Merge frequently, test automatically                       |
| **Refactoring**               | Improve structure without changing behavior                |


## Why It Matters for Software Craftsmanship

XP is the **foundation** that most modern software craftsmanship practices build upon. The SOLID book uses XP as the baseline methodology — TDD, emergent design, simple design, and coding standards all come from XP.

Understanding XP means understanding *why* we do things like write tests first, refactor aggressively, and value consistency.

## Related

- [Simple Design](./simple-design.md)
- [TDD](./tdd.md)
- [Coding Standards](./coding-standards.md)
- [Emergent Design](./emergent-design.md)

