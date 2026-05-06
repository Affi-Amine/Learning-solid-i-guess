# Anti-Patterns

## Origin

The term **anti-pattern** was popularized by Andrew Koenig in 1995 (*Journal of Object-Oriented Programming*) and later expanded in the book *AntiPatterns* by Brown, Malveau, McCormick, and Mowbray (1998). It draws on the Gang of Four's pattern format but inverted — recurring solutions that produce **negative consequences**.

## What They Are

A solution that:

1. Is applied repeatedly to similar problems
2. Looks effective at first
3. Produces more harm than good

Unlike a **code smell** (a hint in existing code), an anti-pattern is a **decision** you should avoid making.

## Comparison

| Code Smell | Anti-Pattern |
|---|---|
| Pattern in existing code | Approach you choose |
| "Look closer here" | "Don't go there" |
| Fix with a refactoring | Fix with rework |
| Local | Often architectural |
| Examples: Long Method, Feature Envy | Examples: God Object, Big Ball of Mud |

## Common Anti-Patterns

### God Object
**What:** One class hoards most responsibilities. All other classes are subservient.
**Why bad:** Single point of change, untestable, low cohesion.
**Avoid:** Distribute responsibilities using RDD.

### Golden Hammer
**What:** "When all you have is a hammer, everything looks like a nail." Forcing a familiar tool into every problem.
**Why bad:** Mismatched solutions; inflexible team thinking.
**Avoid:** Evaluate alternatives. Match tools to NFRs.

### Big Ball of Mud
**What:** No discernible architecture. Just files calling files.
**Why bad:** Unknowable system; every change is dangerous.
**Avoid:** Define layers and boundaries early (clean/hexagonal).

### Lava Flow
**What:** Outdated code retained "just in case" — usually because no one knows what it does.
**Why bad:** Confuses readers; hides the real flow.
**Avoid:** Delete fearlessly with version control + tests as safety net.

### Spaghetti Code
**What:** Control flow that jumps unpredictably. No clear sequence.
**Why bad:** Cognitive overload; impossible to follow.
**Avoid:** Use clear control styles (centralized / delegated / dispersed).

### Copy-Paste Programming
**What:** Duplicated logic instead of shared abstractions.
**Why bad:** Bug fixes only happen in some copies; silent divergence.
**Avoid:** Apply Rule of Three; extract once duplication appears 3 times.

### Magic Numbers / Magic Strings
**What:** Literals scattered through code (`if (x === 7) ...`).
**Why bad:** Unclear meaning; changes require grepping.
**Avoid:** Replace with named constants or value objects.

### Premature Optimization
**What:** Optimizing before measuring or before correctness.
**Why bad:** Adds complexity for no benefit. "Root of all evil" — Knuth.
**Avoid:** Make it work, make it right, then make it fast.

### Vendor Lock-In
**What:** Coupling the entire codebase to one vendor's API.
**Why bad:** Migration becomes effectively impossible.
**Avoid:** Hide vendors behind ports/adapters (clean architecture).

## Key Insight

**Anti-patterns are tempting because they work in the short term.** A God Object is faster to write than five well-designed classes. Spaghetti is faster than thinking through control flow. The cost arrives later — and by then, fixing it is rework, not refactoring.

## How To Avoid Them

1. **Recognize the pattern early** — name it when you see it ("this is becoming a God Object")
2. **Trust the design rules you've learned** — RDD, calisthenics, simple design
3. **Pair / review** — a second set of eyes spots anti-patterns the author can't
4. **Refactor immediately** — anti-patterns calcify quickly

## Related

- [Code Smells](code-smells.md) — anti-patterns' more local cousins
- [Code Smell Categories](code-smell-categories.md) — five categories of smaller-scale issues
- [Object Calisthenics](object-calisthenics.md) — strict habits that prevent most of these
- [Responsibility-Driven Design](responsibility-driven-design.md) — the alternative to God Object thinking
- [Clean Architecture](clean-architecture.md) — the alternative to Big Ball of Mud
