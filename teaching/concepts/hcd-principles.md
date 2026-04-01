# The 7 Fundamental Design Principles

**Origin**: Don Norman, "The Design of Everyday Things"

## Overview

Seven principles that fix problems at any stage of human interaction. Four improve **discoverability** (feedforward), two improve **understanding** (feedback), and one is the umbrella.

## Affordances

**What actions are possible**, communicated by the physical properties of the object.

- A button affords pushing. A handle affords gripping.
- In code: TypeScript *affords* interfaces and abstract classes. JavaScript does not *afford* the `abstract` keyword.
- Your language choice determines what design patterns are even possible.

## Signifiers

**Where and how** to act, communicated by labels, marks, or patterns.

- Intentional: `UserController` (pattern name in class name), BDD test descriptions
- Accidental: dead code signals work-in-progress, thin controllers signal robust architecture
- Signifiers are cheap — good naming is the easiest signifier to add

## Constraints

**Limit** possible actions so you do the right thing.

Four types:

- **Physical**: `const` can't be redeclared, `static` accessed only through class
- **Cultural**: coding conventions, community standards
- **Semantic**: Value Objects enforce domain rules via factory methods
- **Logical**: type checking catches illegal operations at compile time

Key application: **thin interfaces** — minimize the public API, encapsulate complexity inside.

## Mapping

The **relationship between controls and what they control**.

Two sub-principles:

- **Grouping**: related things together (high cohesion)
- **Proximity**: controls near what they control (no anemic domain models)

Best: mount the control directly on the item. Next best: as close as possible. Minimum: same spatial arrangement.

## Feedback

**Immediate communication** of the result of an action.

- Compile-time type errors, test results (red/green), autocomplete, pre-commit hooks
- Must be immediate — delayed feedback causes users to retry or assume failure
- Two error types: **slips** (right goal, wrong sequence) vs **mistakes** (wrong goal entirely)

## Conceptual Models

The **mental model** built from experience using something.

- You don't need to know React's internals, just "re-renders on state change"
- Good conceptual models let you predict effects of actions
- All other principles feed into building the right conceptual model

## Discoverability

The **umbrella principle** — can the user figure out what actions are possible? All other feedforward principles (affordances, signifiers, constraints, mapping) contribute to discoverability.

## Related

- [Human-Centered Design](./human-centered-design.md) — the philosophy these principles belong to
- [Conceptual Models](./conceptual-models.md) — deeper dive
- [Thin Interfaces](./thin-interfaces.md) — key application of constraints

