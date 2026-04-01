# Domain Events

**Origin**: Eric Evans, "Domain-Driven Design" (2003); expanded by Vaughn Vernon

## What It Is

A **Domain Event** is a record that something meaningful happened in the domain. It's written in **past tense**: `OrderPlaced`, `UserRegistered`, `PostUpvoted`.

## Why It Matters

Events are how you **decouple features** while keeping them connected. Instead of one giant function that does everything "after X happens," each reaction is a separate use case subscribed to an event.

## Before vs. After Events

```typescript
// Without events — tightly coupled, grows forever
function afterJobPosted(jobId) {
  chargeCustomer(jobId);
  postToSocial(jobId);
  sendEmail(jobId);
  rebuildSite(jobId);
  // ... and more
}

// With events — each reaction is independent
// Command publishes: JobPosted
// Subscribers: ChargeCustomer, PostToSocial, SendEmail, RebuildSite
```

## Commands vs. Events

| | Commands | Events |
|---|---|---|
| Tense | Imperative present: `createUser` | Past: `UserCreated` |
| Intent | "Do this" | "This happened" |
| Direction | Sent to one handler | Published to many subscribers |
| Failure | Can fail and return errors | Already happened — reactions may fail independently |

## The Temporal Aspect

Real-world processes have a sequence. A washing machine goes `OFF → ON → WASH`, never `OFF → WASH → ON`. Events capture this temporal ordering of features in the domain.

## Key Concerns

- **Persistence**: Events must be saved at the same time as the data changes (Transactional Outbox pattern)
- **Ordering**: Some events must be processed in order
- **Idempotency**: Subscribers should handle receiving the same event twice gracefully

## Related

- [DDD](./ddd.md) — events are a core DDD building block
- [Feature-Driven Structure](./feature-driven-structure.md) — events connect feature folders
- [CQS](./cqs.md) — commands produce events; queries don't
- [Either Pattern](./either-pattern.md) — command results signal when to publish events
