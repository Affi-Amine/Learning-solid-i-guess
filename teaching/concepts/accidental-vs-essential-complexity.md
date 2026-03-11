# Accidental vs. Essential Complexity

**Origin**: Fred Brooks, "No Silver Bullet" (1986)

## Definitions

**Essential complexity** = complexity inherent to the problem itself. If you're building a banking system, you *must* handle transactions, accounts, interest rates, regulations. That's the domain. You can't simplify it away.

**Accidental complexity** = complexity introduced by your *solution*, not required by the problem. Bad abstractions, wrong tool choices, unnecessary indirection, over-engineering — all accidental.

## Examples

| Essential | Accidental |
|---|---|
| Business rules for loan approval | 17 layers of abstraction to check one rule |
| Validating user input | A custom validation framework for 3 form fields |
| Handling concurrent requests | Race conditions from a poorly chosen architecture |
| Calculating tax | A Tax class with 40 methods when you need 3 |

## The Goal

**Minimize accidental complexity. Accept essential complexity.**

You can't make a complex domain simple — but you can stop making it *harder than it needs to be*.

## How Accidental Complexity Creeps In

- Over-engineering ("we might need this someday")
- Wrong abstractions (DRY applied too aggressively)
- Resume-driven development (using tech because it's cool)
- Ignoring the domain (technical solution that doesn't match the business)
- Cargo culting (copying patterns without understanding why)

## The Test

When you look at a complex piece of code, ask:

> "Is this complexity because the *problem* is hard, or because I *made it* hard?"

If the answer is the latter — simplify.

## Related

- [Simple Design](./simple-design.md) — "fewer elements" fights accidental complexity
- [Code Smells](./code-smells.md) — often symptoms of accidental complexity
