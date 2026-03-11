# CQS (Command Query Separation)

**Origin**: Bertrand Meyer, "Object-Oriented Software Construction" (1988)

## What It Is

Every method should be either a **command** or a **query**, but not both.

| Type | Does | Returns | Example |
|---|---|---|---|
| **Command** | Performs a side effect | Nothing (or just an ID) | `createUser(props)` |
| **Query** | Returns data | The requested data | `getUserById(id)` |

## The Rule

- Commands **change state** but return nothing
- Queries **return data** but change nothing

A method that does both is harder to reason about because calling it has hidden effects.

## Why It Matters

- **Predictability**: reading a query is safe, calling a command has consequences
- **Naming**: commands use verbs (`create`, `delete`, `update`), queries use getters (`get`, `find`, `list`)
- **Testing**: queries are easy to test (assert return value), commands need state verification
- **Feedback**: in HCD terms, no return = success feedback for commands; data return = success for queries

## Example

```typescript
class UserRepo {
  // Command — changes state, returns nothing meaningful
  createUser(user: User): Promise<void> { ... }

  // Query — returns data, changes nothing
  getUserById(id: UserId): Promise<User> { ... }
}
```

## When to Break It

Sometimes it's pragmatic to return data from a command (e.g., returning the created entity's ID). The principle is a guideline — the goal is clarity, not dogma.

## Related

- [Coding Standards](./coding-standards.md) — CQS is a naming and design convention
- [HCD Principles](./hcd-principles.md) — CQS creates clear feedback patterns
