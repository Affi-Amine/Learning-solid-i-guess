# Object Stereotypes

## Origin

Formalized by **Rebecca Wirfs-Brock** in *Object Design: Roles, Responsibilities, and Collaborations* (2002). Provides a vocabulary for the recurring patterns of objects you find in OO systems.

## What It Is

Six standard categories that nearly every object falls into. Each stereotype describes the kind of work an object is responsible for.

| # | Stereotype | One-line Job |
|---|---|---|
| 1 | **Information Holder** | Holds state |
| 2 | **Structurer** | Maintains relationships and invariants |
| 3 | **Service Provider** | Performs specialized computation |
| 4 | **Coordinator** | Passes information between objects |
| 5 | **Controller** | Drives a feature / use case |
| 6 | **Interfacer** | Bridges between neighborhoods |

## Why Use Stereotypes

| Without Stereotypes | With Stereotypes |
|---|---|
| Each new class is a one-off | Reach for a known pattern |
| Hard to spot misplaced responsibilities | "These belong to a Service Provider, not a Holder" |
| Vague names (`Manager`, `Helper`) | Names hint at role (`Repository`, `Presenter`) |
| Cohesion accidental | Cohesion designed |

## The Six in Detail

### 1. Information Holder

Holds data. Often immutable.

**Examples:** Value Objects, DTOs, configuration objects.

```typescript
class Money {
  constructor(readonly amount: number, readonly currency: string) {}
}
```

### 2. Structurer

Maintains relationships between other objects and protects invariants.

**Examples:** Aggregates (DDD), connection pools, caches.

```typescript
class Order {
  // Aggregate root: enforces "total = sum of line totals" invariant
  constructor(private lines: OrderLine[]) {}
  total() { return this.lines.reduce((s, l) => s + l.total(), 0); }
}
```

### 3. Service Provider

Specialized computation. Three subtypes:

| Subtype | Example |
|---|---|
| **Stable utility** | `DateUtil`, `TextUtil` |
| **Pure fabrication / Domain Service** | `PriceCalculator`, `TaxPolicy` |
| **Cross-cutting concern** | `Logger`, `AuthGuard`, `Tracer` |

### 4. Coordinator

Passes information between objects so they can do work. Usually thin — delegates everything.

```typescript
class CheckoutCoordinator {
  async run(cart: Cart) {
    const order = await this.orderUseCase.place(cart);
    await this.notifier.notify(order);
    return order;
  }
}
```

### 5. Controller (Use Case)

Application-layer feature driver. Same as the Use Case pattern.

```typescript
class PlaceOrderUseCase {
  async execute(cmd: PlaceOrderCommand) { /* orchestrates domain + infra */ }
}
```

### 6. Interfacer

Bridges between neighborhoods.

| Subtype | Bridges |
|---|---|
| **Internal Interfacer** | Component facade |
| **Gateway** | External APIs |
| **Repository** | Persistence |
| **Presenter** | Domain → UI |
| **Event Listener** | UI → app |

## Combinations

A class can hybridize stereotypes. A `CachingRepository` is **Interfacer + Structurer**. A `LoggingDecorator` adds Service Provider behavior to any role.

Use combinations sparingly — too many means low cohesion.

## How to Use Them

1. List object candidates (CRC cards / sketches)
2. For each candidate, ask: "Which stereotype fits best?"
3. If multiple fit equally, consider splitting
4. Name the class to hint at its stereotype (`...Repository`, `...UseCase`, `...Presenter`)
5. Sanity check: do the responsibilities match the stereotype?

## The Key Insight

**Most objects you'll ever build are one of six things.** Knowing the six saves you from reinventing role categories every time, and makes design conversations dramatically more efficient.

## Related

- [Responsibility-Driven Design](responsibility-driven-design.md) — the philosophy stereotypes serve
- [CRC Cards](crc-cards.md) — stereotype field is implicit in card-naming
- [Value Objects](value-objects.md) — Information Holders done right
- [Anemic Domain Model](anemic-domain-model.md) — what happens when everything becomes an Information Holder
- [Clean Architecture](clean-architecture.md) — layers map roughly to stereotypes
