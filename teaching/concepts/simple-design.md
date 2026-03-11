# Simple Design

**Origin**: Kent Beck, Extreme Programming (XP)

## The Four Elements (in order)

1. **Runs all tests** — Code must work, and you must be able to prove it
2. **Contains no duplication** — DRY (Don't Repeat Yourself)
3. **Maximizes clarity** — Expressive, readable, reveals intent
4. **Has fewer elements** — Minimal lines, methods, classes — only what's needed

## Why Order Matters

The elements are applied **sequentially**, not picked from a menu:

- You can't refactor for clarity if tests don't pass
- You handle duplication before clarity because removing duplication often reveals the right abstractions
- "Fewer elements" comes last because it's a check against over-engineering during the previous steps

## In Practice

Within a TDD workflow:

1. Write a test → make it pass (element 1)
2. See duplication? Refactor it out (element 2)
3. Is the code clear? Rename, restructure (element 3)
4. Did you add unnecessary code? Remove it (element 4)
5. Repeat

## The Key Insight

Simple Design is the industry's **best consensus definition** of clean code. It's not about cleverness or elegance — it's about code that works, is unique, is clear, and is minimal.

> "Humans tend to want to add elements instead of subtracting them to solve problems." — Nature (2021)

Simple Design fights this instinct by making "fewer elements" an explicit rule.

## Related

- [TDD](./tdd.md) — the workflow that makes Simple Design practical
- [Emergent Design](./emergent-design.md) — design that emerges from applying Simple Design iteratively
- [Code Smells](./code-smells.md) — signals that Simple Design rules are being violated

