# Object Capabilities

## Origin

Articulated in **Rebecca Wirfs-Brock**'s *Object Design* (2002) as the four fundamental things objects exist to do.

## What They Are

Every object exists to do one or more of these four things:

| # | Capability | Description | Example |
|---|---|---|---|
| 1 | **Know information** | Hold state | `User` knows email, prefs |
| 2 | **Make decisions** | Apply rules to state | `Order.calculateTotal()` |
| 3 | **Advertise services** | Public methods others can call | `repo.save(order)` |
| 4 | **Maintain connections** | Collaborate via composition / delegation | `Order` holds a `PricingPolicy` |

These four capabilities are what make the four classical OO concepts possible:

| Capability | Enables |
|---|---|
| Know + Decide | **Encapsulation** (state + behavior together) |
| Advertise | **Abstraction** (interface vs implementation) |
| Connect | **Composition** + **Polymorphism** |
| Connect (specific kind) | **Inheritance** |

## Why It Matters

When designing a class, ask which capabilities it needs. If it has only one — usually "knows" — you may have an [Anemic Domain Model](anemic-domain-model.md).

| Healthy Object | Anemic Object |
|---|---|
| Knows AND decides AND collaborates | Only knows |
| Behavior lives with the data | Behavior lives in services elsewhere |
| Methods reveal intent | Methods are just getters/setters |

## Examples

### Healthy

```typescript
class Order {
  // Knows
  private items: Item[] = [];
  private status: OrderStatus = 'pending';

  // Decides
  canAddItem(item: Item): boolean {
    return this.status === 'pending' && !this.containsItem(item);
  }

  // Advertises
  addItem(item: Item) {
    if (!this.canAddItem(item)) throw new Error('cannot add');
    this.items.push(item);
  }

  // Maintains connections — collaborates with PricingPolicy
  total(pricing: PricingPolicy) {
    return pricing.priceFor(this.items);
  }
}
```

### Anemic (anti-example)

```typescript
class Order {
  items: Item[];                    // knows only
  status: string;
  // No decisions, no behavior. All logic lives in OrderService elsewhere.
}
```

## How To Use This Lens

When reviewing code, ask of each class:
- Does it **know** something meaningful?
- Does it **decide** something based on that knowledge?
- What does it **advertise** to the rest of the system?
- Who does it **collaborate** with, and why?

If a class only ticks one box, consider whether the others can be brought in (rather than spread across services and helpers).

## The Key Insight

**Objects without behavior are records.** A class that only knows is a struct dressed up. Real objects also decide, advertise, and connect — that's where their value comes from.

## Related

- [Responsibility-Driven Design](responsibility-driven-design.md) — turns capabilities into design moves
- [Anemic Domain Model](anemic-domain-model.md) — the failure mode when capabilities are stripped
- [Polymorphism](polymorphism.md) — built on the "advertise" + "connect" capabilities
- [Encapsulation](object-stereotypes.md) — built on "know" + "decide" together
