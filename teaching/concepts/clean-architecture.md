# Clean Architecture / Layered Architecture

**Origin**: Robert C. Martin ("Clean Architecture", 2017). Also known as Hexagonal Architecture (Alistair Cockburn, 2005), Onion Architecture (Jeffrey Palermo, 2008), Ports & Adapters.

## What It Is

An architectural pattern that separates **core code** (business logic) from **infrastructure code** (database, web, cache) using layers and dependency inversion. The core has zero knowledge of the infrastructure.

## The Layers

| Layer | Contains | Depends On |
|---|---|---|
| **Domain** (innermost) | Entities, Value Objects, business rules, invariants | Nothing |
| **Application** | Use Cases, application services | Domain only |
| **Adapter** | Interfaces (ports) that define what infrastructure must provide | Application + Domain |
| **Infrastructure** (outermost) | Controllers, DB adapters, web server, cache, APIs | Everything |

## The Dependency Rule

Dependencies point **inward only**. Inner layers never know about outer layers.

- Domain cannot import Application code
- Application cannot import Infrastructure code
- Infrastructure implements interfaces defined in the Adapter layer

## Ports & Adapters

- **Port** = the interface (e.g., `IUserRepo`)
- **Adapter** = the implementation (e.g., `SequelizeUserRepo`, `MockUserRepo`)

This creates a plugin architecture: swap adapters without touching core code.

## Why It Matters

| Without Clean Architecture | With Clean Architecture |
|---|---|
| Features coupled to database | Features are pure, testable code |
| Can only do slow E2E tests | Can unit test business logic |
| Changing DB means changing features | Swap DB adapter, features unchanged |
| Hard to understand what the system does | Domain layer reads like the business |

## Core Code vs Infrastructure Code

| Core | Infrastructure |
|---|---|
| Features, business rules, domain logic | Database, web server, file system, cache |
| Pure — no I/O | Connects core to the real world |
| Unit testable (milliseconds) | Integration testable (seconds) |

## Related

- [Dependency Injection](./dependency-injection.md) — the mechanism for passing adapters into core code
- [Polymorphism](./polymorphism.md) — interfaces enable the port/adapter pattern
- [Transaction Script vs Domain Model](./transaction-script-vs-domain-model.md) — clean architecture uses Domain Model
- [Feature-Driven Structure](./feature-driven-structure.md) — use cases organized by feature within layers
- [Subdomains](./subdomains.md) — modules within a modular monolith
