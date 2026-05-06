# Object Calisthenics

## Origin

Coined by **Jeff Bay** in *The ThoughtWorks Anthology* (2008). Inspired by gymnastics calisthenics — repetitive, simple exercises that build core strength.

## What It Is

A set of **nine self-imposed constraints** for OO code. Following them strictly produces small, focused, expressive classes. They're **training rules** — apply them rigidly while learning, then relax intentionally for real code.

## The Nine Rules

| # | Rule | What It Prevents |
|---|---|---|
| 1 | One indent level per method | Tangled nested logic |
| 2 | Don't use `else` | Cognitive branching cost |
| 3 | Wrap all primitives and strings | Primitive obsession |
| 4 | First-class collections | Scattered collection logic |
| 5 | One dot per line | Law of Demeter violations |
| 6 | Don't abbreviate | Hidden domain concepts |
| 7 | Keep all entities small | Bloated classes/methods |
| 8 | No more than 2 instance variables | Low cohesion / multi-responsibility |
| 9 | No naive getters/setters | Anemic / leaky encapsulation |

## When To Apply

During the **Refactor** step of TDD. Once a test passes:

```
1. Did indentation creep up? → Extract method
2. Used else? → Early return or polymorphism
3. Primitive carrying domain meaning? → Wrap in value object
4. Collection logic in services? → First-class collection
5. Chained dots? → Add a method to the receiver
6. Abbreviated name? → Rename
7. Class > 100 lines / method > 10 lines? → Split
8. 3+ instance variables? → Group into value objects
9. Naive getter/setter? → Replace with intent-revealing method
```

## Comparison

| Without Calisthenics | With Calisthenics |
|---|---|
| Methods sprawl with nested loops | Methods do one thing |
| `string`/`number` carry domain meaning | Value objects enforce invariants |
| Logic spreads across services | Behavior lives with data |
| Long chained calls | Tell, don't ask |
| Cryptic abbreviations | Domain names |

## Acceptable Violations

| Rule | Acceptable When |
|---|---|
| 1 — One indent | Performance-critical hot loops |
| 2 — No else | Symmetric branches read more naturally |
| 5 — One dot | Builder / fluent API |
| 8 — Two fields | Aggregates with genuine multiple parts |
| 9 — No getters | Read-only views for serialization |

You should be able to **defend** every violation.

## The Key Insight

**Constraints are easier than judgment.** Once you've internalized "no nesting," you stop reaching for nested code. The rules become muscle memory; eventually you don't need them — your default is already what they enforced.

## Related

- [Code Smells](code-smells.md) — calisthenics is a smell-prevention list
- [Primitive Obsession](primitive-obsession.md) — Rule 3
- [Law of Demeter](law-of-demeter.md) — Rule 5
- [Tell Don't Ask](tell-dont-ask.md) — Rules 5 & 9
- [Value Objects](value-objects.md) — Rule 3's mechanism
- [Coupling and Cohesion](coupling-and-cohesion.md) — what most rules serve
- [Simple Design](simple-design.md) — calisthenics aligns with all four rules
