# Tell, Don't Ask

## Origin

Coined by **Alec Sharp** in *Smalltalk by Example* (1997) and popularized by Andy Hunt and Dave Thomas (*The Pragmatic Programmer*). A guideline for writing OO code that respects encapsulation.

## What It Says

**Tell** an object what to do, instead of **asking** it for data and acting on the data yourself.

| Asking | Telling |
|---|---|
| `if (account.getBalance() > x) account.setBalance(...)` | `account.withdraw(x)` |
| Caller decides with the data | Object decides with its own data |
| Logic outside the object | Logic inside the object |

## Why It Matters

| Without Tell-Don't-Ask | With Tell-Don't-Ask |
|---|---|
| Logic spread across callers | Logic centralized in objects |
| Anemic domain model | Rich domain model |
| Easy to bypass invariants | Invariants enforced inside the object |
| Refactor breaks every caller | Refactor stays inside one class |

## Examples

### Asking (poor)

```typescript
class Account {
  getBalance(): number { return this.balance; }
  setBalance(b: number) { this.balance = b; }
}

// Every caller must remember the rule:
if (account.getBalance() >= amount) {
  account.setBalance(account.getBalance() - amount);
} else {
  throw new Error("insufficient funds");
}
```

The "balance must be sufficient" rule lives in **every caller**. Forget it once → bug.

### Telling (good)

```typescript
class Account {
  private balance: number;

  withdraw(amount: number): void {
    if (this.balance < amount) throw new Error("insufficient funds");
    this.balance -= amount;
  }

  // No setBalance. No naive getBalance for write-driving logic.
}

account.withdraw(amount);   // rule lives in Account
```

The rule lives **once**, inside `Account`. Callers can't break it.

## Reasonable Exceptions

| Situation | Why It's OK to Ask |
|---|---|
| Display in UI | Need raw data for rendering |
| Serialization (JSON, DB row) | Need to extract state |
| Reporting / analytics | Aggregating across many objects |
| Read models in CQRS | Read side intentionally exposes data |

When asking, prefer **read-only** access — never let the caller mutate.

## Smell Detector

Look at any code that does:

```
let x = obj.getX();
let y = obj.getY();
if (x > y) {
  obj.setSomething(x - y);
}
```

The block usually belongs as a method on `obj`.

## The Connection to Object Capabilities

Tell-Don't-Ask is what you get when you remember objects exist to:

1. Know
2. **Decide** ← this is the one you skip when you "ask"
3. Advertise
4. Maintain connections

When you ask for data and decide outside, you've taken the "decide" capability away from the object.

## Related Patterns

| Pattern | Connection |
|---|---|
| **Law of Demeter** | Tells you not to reach; Tell-Don't-Ask tells you not to extract |
| **Encapsulation** | The OO concept this principle defends |
| **Anemic Domain Model** | The anti-pattern that emerges from constant asking |
| **Command Pattern** | A formalization of "tell the object what to do" |

## The Key Insight

**An object's value is its ability to decide.** If you keep asking objects for data and making decisions outside them, you've reduced them to records — and you've moved logic to places where it can't be tested in isolation.

## Related

- [Law of Demeter](law-of-demeter.md) — its sibling principle
- [Object Capabilities](object-capabilities.md) — "decide" is the capability Tell defends
- [Anemic Domain Model](anemic-domain-model.md) — the failure mode
- [Object Calisthenics](object-calisthenics.md) — Rules 5 and 9 directly enforce this
- [CQS](cqs.md) — Command-Query Separation classifies "tell" vs "ask" precisely
