# Emergent Design

## What It Is

Design decisions **emerge gradually** through iterative development (TDD cycles, pair programming feedback) rather than being decided all upfront.

## Emergent vs. Big Design Up Front (BDUF)


|               | Emergent Design              | BDUF                             |
| ------------- | ---------------------------- | -------------------------------- |
| **When**      | Decisions made as you go     | All decisions made before coding |
| **Who**       | The team, collaboratively    | Often a single architect         |
| **Artifacts** | Working, tested code         | UML diagrams, design docs        |
| **Feedback**  | Continuous, fast             | Late, expensive                  |
| **Risk**      | Small mistakes, caught early | Big mistakes, caught late        |


## How It Works

1. Write a small test
2. Make it pass with simple code
3. Notice a design problem (duplication, poor naming, coupling)
4. Refactor to fix it
5. The design is now slightly better than before
6. Repeat — the design **emerges**

## The Key Benefit

You get **many opportunities to correct bad design** before it hardens into something expensive to change. Each TDD cycle is a checkpoint.

## The Anti-Pattern: Ivory Tower Architect

An architect who designs the entire system in isolation, hands down UML diagrams to developers, and never writes code. This is what emergent design explicitly rejects.

## Important Nuance

Emergent design doesn't mean **no** upfront thinking. You still need:

- A rough architectural direction
- Agreement on major technology choices
- Domain understanding

What you *don't* need is every class, interface, and relationship mapped out before writing line 1.

## Related

- [TDD](./tdd.md) — the primary mechanism for emergent design
- [Simple Design](./simple-design.md) — the rules that guide each refactoring step

