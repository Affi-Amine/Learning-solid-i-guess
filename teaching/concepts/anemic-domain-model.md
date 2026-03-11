# Anemic Domain Model

**Origin**: Martin Fowler identified this as an anti-pattern in 2003.

## What It Is

A domain model where objects hold **only data** (properties/getters/setters) and all behavior lives in separate "service" or "manager" classes. The model is "anemic" because it has no behavior — it's just a data bag.

## The Problem

```typescript
// Anemic: User is just a data bag
class User {
  public name: string;
  public email: string;
  public role: string;
}

// All logic lives far away in a separate class
class UserManager {
  create(user: User) { ... }
  updateRole(user: User, role: string) { ... }
  deactivate(user: User) { ... }
}
```

This violates the **mapping** principle from HCD: the controls (`UserManager` methods) are far from the item being controlled (`User`). It also breaks **encapsulation** — anyone can set `user.role` directly, bypassing any validation.

## The Fix: Rich Domain Model

```typescript
class User {
  private constructor(
    private name: string,
    private email: Email,
    private role: Role
  ) {}

  static create(name: string, email: string): User { ... }
  changeRole(newRole: Role): void { ... }
  deactivate(): void { ... }
}
```

State and behavior live together. The controls are mounted directly on the item they control.

## Why It Matters

- **Duplication**: without behavior on the model, multiple services end up reimplementing the same logic
- **No encapsulation**: anyone can modify internal state without going through business rules
- **Poor discoverability**: to find what you can do with a `User`, you have to search for every class that operates on it

## When Anemic Models Are OK

- Simple CRUD apps with no real business logic
- DTOs (Data Transfer Objects) that explicitly exist just to carry data across boundaries

## Related

- [HCD Principles](./hcd-principles.md) — mapping (grouping + proximity)
- [Coupling & Cohesion](./coupling-and-cohesion.md) — anemic models have low cohesion
