# Domain-Driven Design (DDD)

**Origin**: Eric Evans, "Domain-Driven Design: Tackling Complexity in the Heart of Software" (2003)

## What It Is

A software design approach that puts the **business domain** at the center of everything. The code should model the real world as closely as possible, using the same language that domain experts (business people) use.

## Core Ideas

### Ubiquitous Language

The team (developers + business experts) agrees on a shared vocabulary. The same words used in meetings are used in the code.

```typescript
// The code reads like the business talks
class Member {
  upvote(post: Post): Upvote { ... }
  downvote(post: Post): Downvote { ... }
}
```

If the business says "member" not "user", the code says `Member` not `User`.

### Bounded Contexts

The same word can mean different things in different parts of the business. A `Job` in HR is different from a `Job` in media processing. Each context has its own model and its own meaning for shared terms.

### Layered Architecture

| Layer | Responsibility | Naming Source |
|---|---|---|
| **Domain** | Core business rules | Real-world concepts (`Invoice`, `Member`) |
| **Application** | Use cases / features | Actions (`CreatePost`, `UpvoteComment`) |
| **Infrastructure** | Technical plumbing | Technical constructs (`UserRepo`, `RedisCache`) |
| **Presentation** | UI / API surface | Routes, controllers, views |

### Key Building Blocks

- **Entities**: objects with identity (a `User` with an ID)
- **Value Objects**: objects defined by their attributes, not identity (`Email`, `Money`)
- **Aggregates**: clusters of entities treated as a unit
- **Repositories**: abstractions for storing/retrieving aggregates
- **Domain Events**: things that happened (`UserCreated`, `OrderPlaced`)

## Why It Matters for Naming

DDD is the source of the book's strongest naming advice: **name things after their domain concepts**. When developers learn the business, the code automatically makes sense. Domain-specific names outlive any developer on the project.

## When to Use DDD

- Complex domains with rich business logic
- Long-lived projects with multiple developers
- When the business rules are the hard part, not the technology

For simple CRUD apps, DDD is over-engineering.

## Related

- [CQS](./cqs.md) — commands and queries map to DDD use cases
- [Feature-Driven Structure](./feature-driven-structure.md) — use case folders align with DDD application layer
- [Coupling & Cohesion](./coupling-and-cohesion.md) — bounded contexts enforce boundaries
- [Accidental vs Essential Complexity](./accidental-vs-essential-complexity.md) — DDD focuses on essential complexity
