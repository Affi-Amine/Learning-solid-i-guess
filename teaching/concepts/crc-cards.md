# CRC Cards

## Origin

Invented by **Ward Cunningham** and **Kent Beck** in the late 1980s as a teaching tool for OO design. Quickly adopted by practitioners as a lightweight design technique.

CRC stands for **Class-Responsibility-Collaboration**.

## What It Is

An index card (physical or virtual) with three sections:

```
+----------------------------------------+
| ClassName                              |
+--------------------+-------------------+
| Responsibilities   | Collaborators     |
| - what it knows    | - who it talks to |
| - what it does     |                   |
+--------------------+-------------------+
```

| Section | Purpose |
|---|---|
| **Top** | The class/object name |
| **Left** | What it's responsible for (knowing or doing) |
| **Right** | Other classes it depends on or talks to |

## Why Use Them

| Without CRC Cards | With CRC Cards |
|---|---|
| Jump straight to code | Sketch design before code |
| Hard to spot bloated classes | Long left column = god class smell |
| Hidden coupling | Long right column = high coupling smell |
| Hard to play "what if" | Move/rewrite cards on the table |

The card's small size is the constraint. If the responsibilities don't fit, the class is doing too much.

## Examples

### Order

```
+----------------------------------------+
| Order                                  |
+--------------------+-------------------+
| Responsibilities   | Collaborators     |
| - knows items      | - PricingPolicy   |
| - knows status     |                   |
| - computes total   |                   |
| - validates items  |                   |
+--------------------+-------------------+
```

### PricingPolicy

```
+----------------------------------------+
| PricingPolicy                          |
+--------------------+-------------------+
| Responsibilities   | Collaborators     |
| - applies discounts| - DiscountRules   |
| - computes total   |                   |
+--------------------+-------------------+
```

## How To Use Them

1. List the requirements
2. Brainstorm candidate classes (one card each)
3. Walk through scenarios — physically move cards to show messages
4. When a class is overloaded, split it
5. When two classes always talk together, consider merging or extracting a third

## Smell Detection

| Symptom | What It Suggests |
|---|---|
| 8+ responsibilities on one card | God class — split it |
| 5+ collaborators on one card | High coupling — break dependencies |
| Card has no responsibilities | Anemic / data holder only |
| Two cards always paired | Likely should be one, or share a third |

## Alternatives

| Tool | When |
|---|---|
| Whiteboard | Group sessions, larger systems |
| Markdown files | Solo work, version controlled |
| draw.io / Excalidraw | Digital sketching, screen sharing |
| UML class diagrams | Formal documentation |

## The Key Insight

**Design happens before code.** CRC cards make design *cheap to play with* — easier to throw away three cards than three TypeScript classes.

## Related

- [Responsibility-Driven Design](responsibility-driven-design.md) — RDD is the philosophy CRC implements
- [Object Design](object-design.md) — CRC is the design-phase tool
- [Coupling and Cohesion](coupling-and-cohesion.md) — what CRC card shape directly reveals
