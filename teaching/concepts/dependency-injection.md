# Dependency Injection (DI)

**Origin**: Martin Fowler coined the term in 2004, but the practice predates the name.

## What It Is

Instead of a class creating its own dependencies, they get **passed in from outside** (injected). The class declares what it needs; someone else provides it.

## Without vs. With DI

```typescript
// Without DI — class creates its own dependency
class OrderService {
  private db = new PostgresDatabase();

  getOrders() {
    return this.db.query("SELECT * FROM orders");
  }
}
```

```typescript
// With DI — dependency is injected
class OrderService {
  constructor(private db: Database) {}

  getOrders() {
    return this.db.query("SELECT * FROM orders");
  }
}
```

## Why It Matters

| Without DI | With DI |
|---|---|
| Tight coupling to a specific implementation | Loose coupling through abstractions |
| Hard to test (need a real database) | Easy to test (inject a fake) |
| Changing the dependency means changing the class | Swap implementations without touching the class |
| Class knows too much about how things are built | Class only knows what it needs |

## The Three Injection Methods

| Method | How | When to Use |
|---|---|---|
| **Constructor injection** | Pass dependency via constructor | Default choice — makes dependencies explicit |
| **Method injection** | Pass dependency as a method parameter | When only one method needs it |
| **Property injection** | Set dependency via a public property | Rarely — makes dependencies optional and easy to forget |

Constructor injection is almost always the right choice. It makes dependencies visible and prevents partial object creation (see [Leaky Abstractions](./leaky-abstractions.md)).

## The Key Insight

DI is not about frameworks or containers. It's about **inverting control** — the class doesn't decide *which* database, logger, or service it uses. The caller decides. This makes the class reusable, testable, and decoupled.

## Connection to Other Principles

- **Dependency Inversion Principle (DIP)**: DI is *how* you implement DIP. DIP says "depend on abstractions, not concretions." DI is the mechanism for passing those abstractions in.
- **Single Responsibility**: A class that creates its own dependencies has two jobs — its actual job plus wiring. DI removes the wiring responsibility.

## Related

- [Coupling & Cohesion](./coupling-and-cohesion.md) — DI is the primary tool for achieving loose coupling
- [Leaky Abstractions](./leaky-abstractions.md) — constructor injection prevents partial object creation
- [TDD](./tdd.md) — DI makes classes testable by allowing fake/mock injection
