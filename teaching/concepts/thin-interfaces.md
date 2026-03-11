# Thin Interfaces

**Origin**: John Ousterhout, "A Philosophy of Software Design" (2018). Also related to Martin Fowler's "Minimal Interface."

## What It Is

When designing a class, module, or API, expose the **minimum public surface area** necessary. Hide everything else. Complexity lives inside the module, not on its face.

## Why

Humans have limited **working memory**. Every public method, property, or option is something the consumer must evaluate. More options = more cognitive load = worse discoverability.

## The Rule

- **Deep modules**: small public interface, lots of functionality hidden inside. Good.
- **Shallow modules**: large public interface, little hidden functionality. Bad — the consumer bears the complexity.

## Examples

| Thin (Good) | Fat (Bad) |
|---|---|
| `fs.readFile(path)` | Exposing buffer allocation, encoding selection, file handle management |
| `array.sort()` | Requiring the caller to implement the sorting algorithm |
| `UserRepository.save(user)` | Exposing SQL query building, connection pooling, transaction management |

## How to Apply

- Default to `private`. Only make things `public` when there's a real consumer need.
- If a method is only called internally, it shouldn't be on the interface.
- If you have 20 public methods on a class, ask: does the consumer really need all 20?

## Related

- [HCD Principles](./hcd-principles.md) — thin interfaces are an application of constraints
- [Coupling & Cohesion](./coupling-and-cohesion.md) — thin interfaces reduce coupling surface
- [Leaky Abstractions](./leaky-abstractions.md) — fat interfaces often leak implementation details
