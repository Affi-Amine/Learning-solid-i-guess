# Responsibility-Driven Design (RDD)

## Origin

Coined by **Rebecca Wirfs-Brock** and Brian Wilkerson in 1989 (paper: "Object-Oriented Design: A Responsibility-Driven Approach"). Modernized in the 2002 book *Object Design: Roles, Responsibilities, and Collaborations* by Wirfs-Brock and Alan McKean.

## What It Is

A design method for OO software that thinks in terms of **what objects must do** and **how they cooperate**, rather than data structures or class hierarchies.

The core conversion:

```
Requirements → Responsibilities → Roles → Collaborations
```

| Term | Meaning |
|---|---|
| **Responsibility** | Something that must be done (knowing or doing) |
| **Role** | A logical category of behavior an object plays |
| **Collaboration** | One role asking another role to do something |

## Comparison

| Data-Driven Design | Responsibility-Driven Design |
|---|---|
| Start from "what data do we have?" | Start from "what must happen?" |
| Tables → entities → CRUD methods | Behavior → roles → collaborators |
| Anemic domain models | Rich domain models with real behavior |
| Procedural code dressed as objects | Objects that hold knowledge AND do work |

## Examples

### Requirement
"Users must be able to place an order with multiple items and have it priced correctly."

### Responsibilities Identified
- Validate that items exist
- Calculate the total
- Apply discounts
- Persist the order

### Roles Assigned
- **Order** — knows its items, calculates totals
- **PricingPolicy** — applies discounts
- **OrderRepository** — persists the order

### Collaborations
- `Order` asks `PricingPolicy.priceFor(items)` and gets back a total
- A use case asks `OrderRepository.save(order)`

### CRC Card

```
+--------------------------------------------+
| Order                                      |
+----------------------+---------------------+
| Responsibilities     | Collaborators       |
| - validate items     | - PricingPolicy     |
| - compute total      |                     |
| - track status       |                     |
+----------------------+---------------------+
```

## Why It Matters

RDD is the philosophical underpinning of:

- **DDD's tactical patterns** — aggregates, entities, value objects are RDD applied to domains
- **Clean / Hexagonal architecture** — ports & adapters are role-based collaborations
- **SOLID principles** — they're shortcuts to "good RDD"
- **Mockist TDD** — you mock collaborators, which means you must have named them

## The Key Insight

**An object isn't its data — it's its responsibilities.** Two classes with identical fields but different responsibilities are different objects. Two classes with identical responsibilities but different fields are the same object wearing different clothes.

## Related

- [Object Design](object-design.md) — RDD is the design phase of Object Design
- [CRC Cards](crc-cards.md) — RDD's primary design tool
- [Anemic Domain Model](anemic-domain-model.md) — what happens when RDD is skipped
- [DDD](ddd.md) — RDD applied to business domains
- [Clean Architecture](clean-architecture.md) — RDD applied at the system boundary level
- [Polymorphism](polymorphism.md) — how roles get filled by interchangeable objects
