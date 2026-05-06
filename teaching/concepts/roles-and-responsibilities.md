# Roles and Responsibilities

## Origin

Core RDD vocabulary from **Rebecca Wirfs-Brock**'s *Object Design* (2002). Reframes OO design from "what classes do I have?" to "who's responsible for what, and how do they cooperate?"

## What They Are

| Term | Meaning |
|---|---|
| **Responsibility** | An obligation to **do** (a task) or **know** (some data) |
| **Role** | A coherent group of related responsibilities |
| **Collaboration** | A role asking another role to perform a responsibility |

A **class** is the implementation of one or more roles.

## Why Separate Roles from Classes

| Role-Centric | Class-Centric |
|---|---|
| Multiple classes can fill one role (polymorphism) | One class, one purpose only |
| Roles named by what they *do* | Classes named by what they *are* |
| Easy to swap implementations | Tight coupling to concrete types |
| Mocks make sense — they fill the role | Mocks feel awkward |

## Examples

### House-Bot Example (Chapter 33)

**Design story:** *"The house-bot learns the house layout, listens for voice commands, navigates rooms, doesn't bump into walls."*

**Responsibilities (do):**
- Turn left / right
- Move forward / back
- Detect wake word
- Play audio response
- Build room layout from pictures

**Responsibilities (know):**
- Layout of each room
- Connections between rooms
- Current room

**Roles:**
- `PathFinder`, `RoomLayout`, `Microphone`, `CommandController`, `Wheels`, `Motor`, `ChangeRoom` (use case), `Blinker`

**Collaborations:**
- `ChangeRoom` asks `PathFinder` for a path
- `ChangeRoom` instructs `Wheels` to move
- `CommandController` asks `Microphone` for input

## Finding Each Element

### Finding Responsibilities

Read the design story. Mark every verb (do) and every noun that holds state (know).

### Finding Roles

For each set of responsibilities, ask:
- Could this be one of the six [object stereotypes](object-stereotypes.md)?
- Are these responsibilities cohesive enough to belong to one role?

### Finding Collaborations

For each responsibility, ask:
- *Doing:* "What other role helps with this task?"
- *Knowing:* "Who else needs this information?"

## The Restaurant Analogy

A restaurant manager short on staff doesn't care if it's Molly, Sam, or a robot waiter — they need a **Server** to fill the role.

```
Server (role)
├── Played by: Molly (Tuesday)
├── Played by: Sam (Wednesday)
└── Played by: RobotWaiter (closing shift)

Responsibilities:
- Take orders
- Deliver food
- Handle payments
- Know table assignments
```

This is real polymorphism — interface types describing roles, with classes filling them.

## The Key Insight

**Objects are role-fillers, not data containers.** Once you think in roles, you naturally write code that's testable (mock the role), flexible (swap the player), and clear (names describe what they *do*).

## Related

- [Responsibility-Driven Design](responsibility-driven-design.md) — the design method
- [Object Stereotypes](object-stereotypes.md) — six standard role categories
- [Polymorphism](polymorphism.md) — the mechanism by which roles get filled
- [CRC Cards](crc-cards.md) — the design tool that captures this vocabulary
- [Thin Interfaces](thin-interfaces.md) — a role's contract should expose only what's needed
