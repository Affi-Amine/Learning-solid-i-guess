# Transaction Script vs. Domain Model

**Origin**: Martin Fowler, "Patterns of Enterprise Application Architecture" (2002)

## Two Ways to Organize Business Logic

| | Transaction Script | Domain Model |
|---|---|---|
| **Structure** | One procedure per request | Objects with state + behavior |
| **Where logic lives** | In controllers/services | In domain objects |
| **Complexity handling** | Works for simple CRUD | Handles complex business rules |
| **Testing** | Hard to unit test in isolation | Easy to unit test domain objects |
| **Growth pattern** | Becomes a mess as rules grow | Scales with complexity |
| **Domain knowledge** | Scattered across procedures | Encapsulated in model |

## Transaction Script

Each request gets its own procedure that does everything: validate, query, mutate, save, respond.

```typescript
// Everything in one function — simple but doesn't scale
function createJob(req, res) {
  // validate input
  // check profile complete
  // query employer from DB
  // save job to DB
  // handle errors
  // return response
}
```

This is what most early-career developers write. It works for trivial apps but collapses under complexity — duplication, nested conditionals, no cohesion.

## Domain Model

Business rules live in domain objects. The use case orchestrates, but the logic belongs to the model.

```typescript
// Use case orchestrates
function createJob(request): CreateJobResult {
  const employer = await employerRepo.findById(request.employerId);
  const job = employer.postJob(request.title, request.details);
  await jobRepo.save(job);
  return success(job.id);
}

// Business rules live in the model
class Employer {
  postJob(title, details): Job {
    if (!this.profileComplete) throw new Error("Complete profile first");
    return Job.create({ title, details, postedBy: this.id });
  }
}
```

## When to Use Which

- **Transaction Script**: Simple CRUD, scripts, small apps with no real business logic
- **Domain Model**: Apps with business rules, validation, temporal workflows, multiple actors

## The Anti-Pattern: Anemic Domain Model

A "domain model" where objects hold only data (getters/setters) and all logic lives in services = worst of both worlds. You have the complexity of a domain model but the fragility of a transaction script.

## Related

- [Anemic Domain Model](./anemic-domain-model.md) — the anti-pattern that results from misapplied domain model
- [DDD](./ddd.md) — DDD formalizes the Domain Model pattern
- [Coupling & Cohesion](./coupling-and-cohesion.md) — domain models have high cohesion; transaction scripts have low
