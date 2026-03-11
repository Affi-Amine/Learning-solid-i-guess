# Human-Centered Design (HCD)

**Origin**: Don Norman, "The Design of Everyday Things" (1988)

## What It Is

A design philosophy that puts users' needs, behavior, and pain points first. Instead of just making things that work, design things that work *for humans*.

For software developers, the "users" are **other developers** — your teammates and future maintainers. The goal: make your codebase easy to discover, understand, and change.

## The Two Goals

Everything in HCD reduces to optimizing two things:

| Goal | Question It Answers |
|---|---|
| **Discoverability** | Can I figure out what's possible and where things are? |
| **Understanding** | Can I build a correct mental model of how this works? |

## The 7 Stages of Action

How humans interact with anything:

1. **Goal** — form what you want
2. **Plan** — figure out options
3. **Specify** — choose an action
4. **Perform** — do it
5. **Perceive** — observe the result
6. **Interpret** — make sense of it
7. **Compare** — does the result match the goal?

Stages 2-4 = feedforward (discovery). Stages 5-7 = feedback (understanding).

When someone gets stuck at any stage, a specific design principle can fix it.

## The Key Insight

Clean code isn't subjective taste — it's measurable through HCD. If another developer can discover what your code does, understand how it works, and change it safely, your design is good. If they can't, you have specific principles to diagnose and fix the problem.

## Related

- [HCD Principles](./hcd-principles.md) — the 7 principles (affordances, signifiers, constraints, mapping, feedback, conceptual models)
- [Developer Experience](./developer-experience.md) — DX is the application of HCD to code
- [Conceptual Models](./conceptual-models.md) — the end goal of good design
