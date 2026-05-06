# Primitive Obsession

## Origin

A **code smell** described by **Martin Fowler** in *Refactoring* (1999). Listed among the most common smells in Fowler's catalog.

## What It Is

The habit of using built-in primitive types (`string`, `number`, `boolean`, `Date`) to represent **domain concepts** that deserve their own type.

## Examples

### Smelly

```typescript
function transfer(amount: number, currency: string, fromUserId: string, toUserId: string) {
  if (amount < 0) throw new Error("Negative amount");
  if (!fromUserId || !toUserId) throw new Error("Missing user");
  // currency check scattered across many call sites
}
```

Problems:
- Validation duplicated wherever amount/userId is used
- `transfer(amount, fromUserId, currency, toUserId)` — wrong order, but compiler is happy
- Domain meaning (`Money`, `UserID`) is implicit

### Healthy

```typescript
class Money {
  constructor(readonly amount: number, readonly currency: string) {
    if (amount < 0) throw new Error("Negative amount");
  }
  add(other: Money): Money {
    if (this.currency !== other.currency) throw new Error("Currency mismatch");
    return new Money(this.amount + other.amount, this.currency);
  }
}

class UserID {
  constructor(readonly value: string) {
    if (!value) throw new Error("UserID required");
  }
}

function transfer(amount: Money, from: UserID, to: UserID) { /* ... */ }
```

| Win | How |
|---|---|
| Validation in one place | The constructor |
| Order errors caught | `transfer(money, userID, userID)` — types prevent swap |
| Behavior lives with data | `money.add(other)`, `money.times(2)` |
| Self-documenting API | `UserID` reads better than `string` |

## When NOT To Wrap

- **Truly anonymous values:** loop indices, array sizes, intermediate sums
- **No domain meaning:** a generic `count` of widgets in a UI list
- **No invariants to enforce:** if a value can legitimately be any string, wrapping adds noise

## Detecting It

Ask:
- Does this primitive have **rules** (range, format, allowed values)?
- Does it appear in **multiple methods** with the same validation?
- Could it have **behavior** (math operations, formatting)?
- Could it be **mistakenly swapped** with another primitive of the same type?

Three or more "yes" answers → wrap it.

## Related Smells

| Smell | Connection |
|---|---|
| **Long Parameter List** | Often caused by passing many primitives |
| **Data Clumps** | Multiple primitives that travel together — wrap them |
| **Feature Envy** | Methods doing logic that belongs on the wrapped type |
| **Shotgun Surgery** | Validation changes hit every call site |

## The Key Insight

**Primitives are the cheapest types — and that's the problem.** When everything is a `string`, your domain disappears into the type system's noise floor. Wrapping makes the domain visible and enforceable.

## Related

- [Value Objects](value-objects.md) — the mechanism for wrapping
- [Object Calisthenics](object-calisthenics.md) — Rule 3 enforces this directly
- [Code Smells](code-smells.md) — the smell catalog
- [Either Pattern](either-pattern.md) — works well with value object validation
