# Subdomains

**Origin**: Eric Evans, "Domain-Driven Design" (2003)

## What It Is

A **subdomain** is a decomposed logical slice of the entire problem domain. Any business can be broken into multiple subdomains, each responsible for a specific set of features.

## Example

A vinyl trading application might decompose into:

| Subdomain | Responsible For |
|---|---|
| **Trading** | Listing vinyl, creating/accepting/declining offers |
| **Billing** | Charging customers, refunds, subscriptions |
| **Shipping** | Shipping labels, tracking, delivery confirmation |
| **Users** | Registration, authentication, profiles |
| **Notifications** | Emails, push notifications |

## Three Types

| Type | What It Is | Strategy |
|---|---|---|
| **Core** | What you're getting paid to build. The competitive advantage. | Build it yourself, invest the most effort |
| **Generic** | Utility concerns that any business needs | Buy off-the-shelf (Auth0, Stripe) or use libraries |
| **Supporting** | Assists the core but isn't the main value | Build simply, don't over-engineer |

Focus on the **core subdomain first**. It's where the essential complexity lives.

## Subdomains Are Never Fully Decoupled

They rely on each other. Use **Context Maps** to make relationships explicit:

- **Customer-Supplier**: upstream provides capabilities, downstream consumes
- **Conformist**: downstream uses upstream's model as-is
- **Anticorruption Layer**: downstream translates upstream's model into its own

## In Code

Subdomains map to **modules** (in a monolith) or **services** (in microservices). Start as a modular monolith — structure the code so it *can* be split later.

```
src/
  modules/
    trading/       ← core subdomain
    billing/       ← generic subdomain
    shipping/      ← supporting subdomain
    users/         ← generic subdomain
```

## Related

- [DDD](./ddd.md) — subdomains are a core DDD concept
- [Event Storming](./event-storming.md) — how subdomains are discovered
- [Feature-Driven Structure](./feature-driven-structure.md) — subdomains map to module folders
- [Coupling & Cohesion](./coupling-and-cohesion.md) — subdomains enforce boundaries
