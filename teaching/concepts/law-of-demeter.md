# Law of Demeter

## Origin

Coined at Northeastern University in 1987 during the **Demeter Project** by Karl Lieberherr and colleagues. Often summarized as **"only talk to your immediate friends."**

## What It Says

A method should only call methods on:

1. Itself
2. Its parameters
3. Objects it creates
4. Its direct fields/components

It should **not** reach into objects to call methods on objects-of-objects.

## The "One Dot" Heuristic

```typescript
// ✗ Reaches through one object to use another
person.getWallet().getCreditCard().charge(50);

// ✓ Single dot per line — direct collaboration
person.chargeCreditCard(50);
```

## Comparison

| Demeter-Violating | Demeter-Friendly |
|---|---|
| `a.b().c().d()` | `a.doSomething()` |
| Caller knows internals of `a` | Caller knows only what `a` exposes |
| Refactor `a` → break callers | Refactor `a` → callers unaffected |

## Why It Matters

| Without Demeter | With Demeter |
|---|---|
| Caller couples to deep structure | Caller couples to direct interface |
| Renaming `Wallet.getCreditCard()` ripples everywhere | Renaming is internal to `Person` |
| Code reads like archaeology | Code reads like instructions |
| Hard to test (must mock 3 deep) | Easy to test (mock one level) |

## Examples

### Violation

```typescript
class OrderProcessor {
  process(order: Order) {
    if (order.getCustomer().getAddress().getCountry() === 'US') {
      // ...
    }
  }
}
```

To test this, you must construct `Order → Customer → Address → Country`. Any change to that chain breaks the processor.

### Fix

```typescript
class Order {
  isShippingTo(country: string): boolean {
    return this.customer.shipsTo(country);
  }
}

class Customer {
  shipsTo(country: string): boolean {
    return this.address.isIn(country);
  }
}

class OrderProcessor {
  process(order: Order) {
    if (order.isShippingTo('US')) {
      // ...
    }
  }
}
```

Each class exposes a meaningful question. The processor doesn't know about `Address`.

## Acceptable Chains

Some chains are NOT Demeter violations:

| Chain | Why It's OK |
|---|---|
| `query.where(...).orderBy(...).limit(...)` | Builder/fluent API — same role |
| `array.filter(...).map(...).reduce(...)` | All return same collection type |
| `list.first().name` | Plain data access, no behavior |

The smell is **calling behavior on objects you reached for**, not all chaining.

## Related Idea: Tell, Don't Ask

```typescript
// Asking — caller decides
if (account.getBalance() > amount) {
  account.setBalance(account.getBalance() - amount);
}

// Telling — object decides
account.withdraw(amount);   // throws if insufficient
```

Demeter and Tell-Don't-Ask both push behavior **inward**.

## The Key Insight

**Don't reach. Ask the object you have for what you need.** If `person.getWallet().charge()` was the answer, the right question was `person.charge()` all along.

## Related

- [Tell Don't Ask](tell-dont-ask.md) — its philosophical sibling
- [Object Calisthenics](object-calisthenics.md) — Rule 5 enforces it
- [Coupling and Cohesion](coupling-and-cohesion.md) — Demeter directly reduces coupling
- [Leaky Abstractions](leaky-abstractions.md) — Demeter violations expose internals
