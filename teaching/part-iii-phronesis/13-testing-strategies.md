# Chapter 25: Testing Strategies

## Core Question

**What do you test, at which scope, and with which type of test?**

A layered architecture unlocks multiple testing options. The strategy: unit test core code, acceptance test features as unit tests, integration test adapters, E2E test for final confidence.

---

## 1. Test Types

| Type | What It Tests | Speed | Scope |
|---|---|---|---|
| **Unit** | Core code (pure, no I/O). Contract of a class/function. | Fast (ms) | Smallest |
| **Integration** | Our code works with code we didn't write (DB, APIs, libraries) | Medium (s) | Middle |
| **End-to-End** | Entire system from a real user's perspective (click, type, see) | Slow (s-min) | Largest |
| **Acceptance** | Feature works per customer specification (Given-When-Then) | Varies by scope | Feature-level |

### Integration Test Flavors

| Flavor | What It Tests |
|---|---|
| **Contract tests** | Concrete adapter implements the interface correctly (e.g., all `Repository` methods work) |
| **Incoming adapter tests** | Request handler (REST, GraphQL) calls the correct use case |
| **Outgoing adapter tests** | External dependency (Stripe, S3) can be connected to and used |

### Acceptance Test Scope Options

| Scope | Pros | Cons |
|---|---|---|
| **E2E** | Covers the most ground | Slow, hard to set up, can't verify everything |
| **Integration (API level)** | Covers front-to-back through API | Still needs infrastructure running |
| **Unit (Use Case level)** | Fast, cheap, tests core logic | Doesn't test infrastructure integration |

The author recommends: **coarse-grained unit tests** through Use Cases. Mock the adapters, test the feature logic.

---

## 2. What Needs Testing?

### Features (Commands)

- Fail when they should fail (correct error for invalid input)
- Succeed when they should succeed
- Adhere to security rules
- Invoke the correct state-changing calls with correct arguments

### Features (Queries)

- Data is visible
- Data is correct
- Security and scope are enforced

### Core Code

- Utilities, value objects, entities, domain services
- Custom auth/middleware logic
- Should rarely need mocks — this code is pure

### Infrastructure

| Dependency Type | What to Test | How |
|---|---|---|
| **Managed** (your DB) | Connection works, repository methods work | Contract tests against real DB |
| **Unmanaged** (external API) | Can connect, can perform needed operations | Real service, sandbox, or fake server |

---

## 3. The Testing Strategy

```mermaid
flowchart TB
    subgraph unit ["Unit Tests (fast, core)"]
        direction TB
        U1["Domain layer code"]
        U2["Value Objects, Entities"]
        U3["Utilities, middleware"]
    end

    subgraph acceptance ["Acceptance Tests (as unit tests)"]
        direction TB
        A1["Use Cases with mocked adapters"]
        A2["Given-When-Then scenarios"]
        A3["Verify state-changing calls were made"]
    end

    subgraph integration ["Integration Tests"]
        direction TB
        I1["Input adapters: API calls correct use case"]
        I2["Output adapters: DB contract tests"]
        I3["External APIs: Stripe sandbox, S3 real"]
    end

    subgraph e2e ["E2E Tests (confidence)"]
        direction TB
        E1["Black box, no mocks"]
        E2["User perspective: click, type, see"]
        E3["Production-like environment"]
    end

    unit ~~~ acceptance
    integration ~~~ e2e
```

### Layer by Layer

| Layer | Test Type | Mocks Needed? |
|---|---|---|
| **Domain** | Unit tests | No — pure code |
| **Application (Use Cases)** | Acceptance tests as unit tests | Yes — mock repositories/adapters with spies |
| **Input adapters (API)** | Integration tests | Stub use case responses |
| **Output adapters (DB)** | Contract tests | No — test against real DB |
| **External APIs** | Integration tests | Real, sandbox, or fake server |
| **Full system** | E2E tests | No — black box |

### Mock Rules

- **Mocks for commands** — verify that state-changing effects happened
- **Stubs for queries** — return canned data without side effects

---

## 4. Managed vs. Unmanaged Dependencies

```mermaid
flowchart LR
    subgraph managed ["Managed (you own it)"]
        direction TB
        M1["Your database"]
        M2["Full control"]
        M3["Contract tests"]
    end

    subgraph unmanaged ["Unmanaged (you don't own it)"]
        direction TB
        U1["Stripe, S3, shared queue"]
        U2["Limited control"]
        U3["Sandbox, fake server, or real"]
    end

    managed ~~~ unmanaged
```

---

## 5. Mental Map

```mermaid
flowchart TB
    TS(["Testing Strategy"])

    TS --> TYPES["Test Types"]
    TYPES --> UNIT["Unit: core code, fast"]
    TYPES --> INT["Integration: adapters"]
    TYPES --> E2E["E2E: user perspective"]
    TYPES --> ACC["Acceptance: features"]

    TS --> WHAT["What to Test"]
    WHAT --> CMD["Commands: fail/succeed/side-effects"]
    WHAT --> QRY["Queries: data correct/visible/secure"]
    WHAT --> INFRA["Infrastructure: connection/contract"]

    TS --> STRAT["The Strategy"]
    STRAT --> DOM["Unit test domain layer"]
    STRAT --> UC["Acceptance test use cases as unit tests"]
    STRAT --> ADAPT["Integration test adapters"]
    STRAT --> FULL["E2E for final confidence"]

    style TS fill:#4a86c8,stroke:#2a5a8c,color:#fff
    style UC fill:#d9ead3,stroke:#090,color:#000
```

---

## Key Takeaways

1. **Unit tests = core code only** — pure, fast, no I/O (Feathers' rule)
2. **Acceptance tests as unit tests** — exercise Use Cases with mocked adapters. The best balance of speed and coverage.
3. **Integration tests for adapters** — contract tests for DB, incoming tests for API, outgoing for external services
4. **E2E tests for confidence** — black box, no mocks, production-like environment, user perspective
5. **Mocks for commands, stubs for queries** — verify state-changing effects happened, return canned data for reads
6. **Managed vs unmanaged** — you own your DB (contract tests). You don't own Stripe (sandbox/real/fake).

---

## Concepts Introduced

No new standalone concepts — this chapter synthesizes:
- [Acceptance Tests](../concepts/acceptance-tests.md) — written at the use case scope
- [Clean Architecture](../concepts/clean-architecture.md) — layers determine which test type to use
- [TDD](../concepts/tdd.md) — double-loop TDD uses this strategy
