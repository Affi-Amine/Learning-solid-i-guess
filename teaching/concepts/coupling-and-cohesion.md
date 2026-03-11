# Coupling & Cohesion

## The North Star of Software Design

> **Loose coupling + High cohesion = Good design**
> **Tight coupling + Low cohesion = Bad design**

Every design decision you make either moves you toward or away from this.

## Coupling

**Coupling** = the degree to which one module depends on another.

| Type | Description | Example |
|---|---|---|
| **Tight coupling** | Module A can't work without Module B | Class directly instantiates its dependencies |
| **Loose coupling** | Modules interact through abstractions | Dependency injection, interfaces |

**Why tight coupling hurts**: Change one thing → ripple effects everywhere. This is the "ripple" complexity signal.

## Cohesion

**Cohesion** = the degree to which elements within a module belong together.

| Type | Description | Example |
|---|---|---|
| **High cohesion** | Everything in the module relates to one purpose | A `UserRepository` that only does user data access |
| **Low cohesion** | Module does many unrelated things | A `Utils` class with email, date, string, and file methods |

**Why low cohesion hurts**: You have to understand things that aren't related. Finding what you need is harder. Changes affect unrelated code.

## The Relationship

They're **inversely related** in practice:
- Improving cohesion (grouping related things) tends to reduce coupling
- Reducing coupling (separating unrelated things) tends to improve cohesion

## Quick Test

Ask yourself:
- **Coupling**: "If I change this module, how many other modules break?" (Fewer = better)
- **Cohesion**: "Does everything in this module relate to one idea?" (Yes = better)

## Related

- [Simple Design](./simple-design.md) — "maximizes clarity" is largely about cohesion
- [Leaky Abstractions](./leaky-abstractions.md) — a form of coupling through implementation details
