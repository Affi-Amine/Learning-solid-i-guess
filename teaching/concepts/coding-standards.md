# Coding Standards

## What It Is

A collection of **rules** that push code toward a consistent style and approach within a codebase. Also called "coding conventions."

## What They Cover

- Project structure and organization
- How to implement new features
- Error handling approach
- Naming conventions
- Formatting and style
- Commit and deployment process
- Comments policy
- File/function size limits

## Why Consistency Is the Magic Word

Humans are **pattern-matching machines**:
- See it once → note it
- See it twice → believe it's the pattern
- See it three times → it's law

Breaking established patterns creates cognitive load because the reader has to figure out if the deviation is intentional and meaningful, or just inconsistency.

## Impact on Complexity

Consistency improves 3 of 4 complexity signals:

| Signal | Improved? | How |
|---|---|---|
| Cognitive load | ✅ | Patterns reduce thinking effort |
| Discoverability | ✅ | Predictable locations for things |
| Understandability | ✅ | Familiar patterns are instantly readable |
| Ripple effects | ❌ | That's a coupling problem, not a consistency one |

## In Practice

- **Linters** (ESLint, Pylint) enforce formatting rules automatically
- **Formatters** (Prettier, Black) remove style debates entirely
- **Architecture Decision Records (ADRs)** document structural decisions
- **Code review** catches deviations that tooling misses
- **Templates/generators** ensure new code follows existing patterns

## Related

- [Extreme Programming](./extreme-programming.md) — XP makes coding standards a core practice
- [Developer Experience](./developer-experience.md) — good standards improve DX
