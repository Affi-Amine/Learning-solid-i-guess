# Polymorphism & Indirection

**Origin**: Concept predates OO (function pointers in C), but made **safe** by OO languages (Alan Kay, 1966)

## What It Is

**Polymorphism** = the ability for an abstraction to take many shapes. You program against an interface, and the actual implementation can be swapped without changing the calling code.

**Indirection** = the architectural technique of depending on an abstraction instead of a concrete implementation. The fourth building block of all software (alongside sequence, selection, iteration).

## Before vs. After Safe Polymorphism

| Before (Structured) | After (OO) |
|---|---|
| Function pointers in C — no compiler checks | Interfaces and abstract classes — compiler-enforced |
| Forget to initialize → hard bugs | Must implement all methods or won't compile |
| Growing switch statements for each new type | New type implements the interface — no switch needed |

## The USB Port Analogy

Instead of writing code for every possible USB device (mouse, keyboard, webcam...), define a **port** (interface) and let device manufacturers write the **adapter** (implementation).

```typescript
interface MIDIDevice {
  sendNote(): void;
  onNote(note: Note): void;
}

// Any device can plug in — just implement the interface
class Drumkit implements MIDIDevice { ... }
class Keyboard implements MIDIDevice { ... }
```

## Why It's the Most Important OO Concept

Polymorphism enables:
- **Dependency Inversion** — depend on abstractions, not concretions
- **Open-Closed Principle** — extend behavior without modifying existing code
- **Testability** — inject fakes/mocks that implement the same interface
- **Plugin architecture** — swap implementations at runtime

## Related

- [Dependency Injection](./dependency-injection.md) — the mechanism for passing in polymorphic dependencies
- [Coupling & Cohesion](./coupling-and-cohesion.md) — polymorphism reduces coupling
- [Thin Interfaces](./thin-interfaces.md) — the interface should be minimal
