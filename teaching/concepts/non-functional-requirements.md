# Non-Functional Requirements (NFRs)

## Origin

Standard term from systems engineering and software architecture. Sometimes called **quality attributes** or **the -ilities** (because they end in "-ility": maintainability, scalability, usability...).

## What It Is

Requirements that describe **how** the system should behave, not **what** it should do.

| Functional Requirements | Non-Functional Requirements |
|---|---|
| "User can place an order" | "Order placement responds in < 200ms" |
| Specific feature behavior | Quality attributes |
| ✅ TDD covers these | ❌ TDD doesn't cover these directly |

## Two Categories

### Execution Qualities (Run-Time)

Visible to users while the system runs.

| Quality | What It Means |
|---|---|
| **Performance** | Response time, throughput |
| **Reliability** | Uptime, fault tolerance |
| **Usability** | Easy to use |
| **Security** | Resists attack and data leaks |
| **Efficiency** | Resource usage |
| **Correctness** | Produces right answers |
| **Scalability** | Handles growth in load |
| **Availability** | Fraction of time it works |

### Evaluation Qualities (Code-Time)

Visible to developers while changing the code.

| Quality | What It Means |
|---|---|
| **Maintainability** | Easy to understand and modify |
| **Testability** | Easy to verify with tests |
| **Flexibility** | Easy to change in unforeseen ways |
| **Reusability** | Components usable in other contexts |
| **Portability** | Runs on different platforms |
| **Modularity** | Cleanly separable parts |

## Why They Matter

| If You Skip NFRs | Result |
|---|---|
| Don't think about scalability | Architecture can't grow with load |
| Don't think about testability | Tests become brittle, slow, painful |
| Don't think about flexibility | Every requirement change is a rewrite |
| Don't think about security | Get hacked |

NFRs **shape architecture** in ways functional requirements don't. They must be discovered **during analysis**, not retrofitted later.

## Discovery

Ask stakeholders questions like:
- How fast must it be?
- How many concurrent users?
- What's the cost of downtime?
- How sensitive is the data?
- How often will requirements change?
- Will we need to port this elsewhere?

## The Key Insight

**Functional requirements get you to "it works." Non-functional requirements get you to "it works *and* it's still working five years from now under load."**

You can't write tests for "maintainability" the way you can for "places orders correctly." NFRs are designed in, not asserted on.

## Related

- [Object Design](object-design.md) — analysis phase must capture NFRs
- [Walking Skeleton](walking-skeleton.md) — exposes NFR feasibility early
- [Clean Architecture](clean-architecture.md) — provides testability and flexibility by design
- [Coupling and Cohesion](coupling-and-cohesion.md) — direct levers on evaluation qualities
