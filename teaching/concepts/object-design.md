# Object Design

## Origin

Term used by **Rebecca Wirfs-Brock** in her 2002 book *Object Design: Roles, Responsibilities, and Collaborations*. Builds on earlier OOAD (object-oriented analysis & design) work from the 1980s-90s.

## What It Is

The full discipline of building object-oriented software. It has **three distinct parts**, each requiring practice:

1. **Analysis** — identify requirements (functional + non-functional)
2. **Design** — convert requirements into roles, responsibilities, collaborations
3. **Programming** — translate designs into classes and objects (usually inside a TDD loop)

Most developers conflate "OO" with step 3 only. That's why their code is messy.

## Comparison

| Just Programming | Full Object Design |
|---|---|
| Jump to classes immediately | Discover requirements first |
| Inheritance feels arbitrary | Roles and collaborations drive structure |
| Mocks/stubs decisions are random | Roles tell you where to mock |
| NFRs ignored or retrofitted | NFRs shape architecture early |
| Refactor reactively | Refactor toward known design intent |

## Examples

### Analysis output
"User must be able to place an order. System must handle 10k orders/sec (NFR: scalability)."

### Design output
- **Order** (responsibility: validate items, compute total; collaborates with **Pricing**, **Inventory**)
- **Pricing** (responsibility: compute discounts; collaborates with **DiscountRules**)
- **Inventory** (responsibility: reserve stock; collaborates with **Warehouse**)

### Programming output
TypeScript classes implementing the design, driven by failing tests.

## Tools by Phase

| Phase | Tools |
|---|---|
| Analysis | Event Storming, Impact Mapping, BDD scenarios, UML sequence diagrams |
| Design | CRC cards, whiteboards, UML class diagrams, markdown sketches |
| Programming | Test framework, IDE, TDD loop, refactoring patterns |

## The Key Insight

**Programming is the *last* step.** If you write code before doing analysis and design, you'll constantly fight the structure rather than express it.

## Related

- [Responsibility-Driven Design](responsibility-driven-design.md) — the design method at the heart of Object Design
- [CRC Cards](crc-cards.md) — primary design-phase tool
- [Non-Functional Requirements](non-functional-requirements.md) — what analysis must capture
- [Simple Design](simple-design.md) — design's quality goalposts
- [TDD](tdd.md) — the loop programming usually runs inside
