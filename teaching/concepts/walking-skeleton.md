# Walking Skeleton

**Origin**: Alistair Cockburn, "Crystal Clear" (2004)

## What It Is

The **simplest possible architecture** that performs a small end-to-end function, runs tests, and can be deployed. It's the platform upon which you write your first acceptance test.

Think of it as the skeleton of your app — no muscles, no skin, but the bones are connected and it can "walk" (run end-to-end).

## What It Includes

- A request hitting the API and returning a response
- The response touching the database (or equivalent persistence)
- Tests that run against this flow
- A build and deploy pipeline that works

## What It Does NOT Include

- Real features or business logic
- Complete UI
- All infrastructure components
- Performance optimization

## Why It Matters

- **Proves architectural components work together** before feature work begins
- **Establishes the testing strategy** — you can't write acceptance tests without infrastructure to run them
- **Eliminates integration surprises** — better to discover that two services can't talk in week 1, not week 10
- **Gives developers a starting point** — everyone can see how a feature flows end-to-end

## Iteration Zero

Often built during a **zero-functionality iteration** — the first sprint where no feature stories are delivered. Instead, time is spent on:

- Testing framework setup
- Automated builds and deployment scripts
- Docker/infrastructure configuration
- Walking skeleton implementation

## Related

- [Acceptance Tests](./acceptance-tests.md) — the walking skeleton enables the first acceptance test
- [Feature-Driven Structure](./feature-driven-structure.md) — the skeleton establishes the folder structure
- [TDD](./tdd.md) — the skeleton proves the test infrastructure works
