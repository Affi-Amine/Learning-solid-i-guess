# Value Objects

**Origin**: Eric Evans, "Domain-Driven Design" (2003)

## What It Is

A **Value Object** is an object defined by its attributes, not by an identity. Two Value Objects with the same attributes are considered equal. They are typically **immutable** — once created, they don't change.

The key design pattern: wrap primitives in domain-specific types with validation enforced at creation time.

## The Problem They Solve

Primitives (`string`, `number`) carry no domain meaning and no validation:

```typescript
// Bad — accepts any string, including empty or invalid ones
function createUser(email: string, password: string): User { ... }

createUser("", ""); // Compiles fine, but meaningless
```

## The Solution

Wrap the primitive in a type that enforces the rules:

```typescript
class Email {
  private constructor(private value: string) {}

  static create(email: string): Email {
    if (!Email.isValid(email)) {
      throw new Error("Invalid email");
    }
    return new Email(email);
  }

  private static isValid(email: string): boolean { ... }

  getValue(): string { return this.value; }
}
```

Now the function signature enforces correctness:

```typescript
function createUser(email: Email, password: Password): User { ... }

// Must pass through factory validation — invalid state is impossible
const email = Email.create("khalil@example.com");
```

## Key Properties

| Property | Why |
|---|---|
| **Immutable** | Once created, the value can't change — prevents bugs |
| **Self-validating** | The factory method enforces all business rules at creation |
| **Private constructor** | Forces creation through the factory — no partial objects |
| **Equality by value** | Two `Email("a@b.com")` are the same, unlike entities |

## Examples

| Primitive | Value Object | Rules It Enforces |
|---|---|---|
| `string` | `Email` | Must contain `@`, valid domain, not empty |
| `string` | `Password` | Minimum length, complexity requirements |
| `number` | `Money` | Non-negative, specific currency |
| `string` | `PostTitle` | Max 200 chars, no empty strings |

## The Key Insight

Value Objects make the **implicit explicit**. Instead of "string-ly typed" code where anything goes, you get domain-typed code where the compiler enforces business rules.

## Related

- [DDD](./ddd.md) — Value Objects are a core DDD building block
- [Leaky Abstractions](./leaky-abstractions.md) — factory methods prevent partial creation
- [HCD Principles](./hcd-principles.md) — Value Objects are constraints that reduce the surface area for misuse
