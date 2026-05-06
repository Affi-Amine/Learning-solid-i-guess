# Transformation Priority Premise (TPP)

## Origin

Coined by Robert C. Martin (Uncle Bob) in 2013. A response to the vague "obvious implementation" advice in classic TDD literature.

## What It Is

A **ranked list of every code transformation** that happens during TDD, ordered from simplest to most complex. When making a failing test pass, prefer the transformation **highest on the list** that still works.

It's a constraint on the "Obvious Implementation" strategy — instead of relying on gut feel, you walk the list.

## The Two Kinds of Change

| | Transformation | Refactoring |
|---|---|---|
| **Affects** | Behavior | Structure only |
| **Phase** | RED → GREEN | After GREEN |
| **Direction** | Specific → generic | Same behavior, cleaner |

## The List

| # | Name | Pattern |
|---|---|---|
| 1 | `{}` → `nil` | Empty body to returning nothing/null/empty |
| 2 | `nil` → constant | Returning a literal value |
| 3 | constant → constant+ | More complex constant or combination |
| 4 | constant → scalar | Use of arguments |
| 5 | statement → statements | Unconditional sequence (assignment, calls) |
| 6 | unconditional → conditional | `if/else`, `switch`, ternary |
| 7 | scalar → array | Indexed lookup |
| 8 | array → container | Object/class wrapper |
| 9 | statement → tail recursion | Recursion that compiles to a loop |
| 10 | `if` → loop | `for`, `while` |
| 11 | statement → recursion | Full (non-tail) recursion |
| 12 | expression → function | Extract subroutine |
| 13 | variable → mutation | Reassignment / state change |

## Why Order Matters

Higher transformations are cheaper to write, easier to extend, and less likely to cause impasses. Mutation is last because state is the source of most bugs.

## Examples

### Add function

```typescript
// Test 1: add(0,0) === 0  →  return 0;             // (2) constant
// Test 2: add(2,3) === 5  →  return x + y;         // (4) scalar
```

### Fibonacci

```typescript
// fib(0) === 0       →  return 0;                                  // (2)
// fib(1) === 1       →  return n === 0 ? 0 : 1;                    // (6)
// fib(5) === 5       →  return n < 2 ? n : fib(n-1) + fib(n-2);    // (11)
```

### Anti-example (impasse-prone)

```typescript
// Test 2: jump straight to a Strategy pattern with three classes.
// Test 5 needs a different shape — now you rewrite everything.
```

## How to Use It

### Going Green
"Can transformation 1 pass this test? No → try 2. Yes → use it."

### Refactoring
Look at your code. Can you replace a step with a higher transformation? Mutation → return value. Loop → map/reduce.

### When Stuck
Revert to last green. Try a transformation higher on the list.

## The Key Insight

**Simpler transformations early prevent expensive rewrites later.** TPP turns "always pick the simplest thing" from a vague principle into a concrete checklist.

## Related

- [TDD](tdd.md) — TPP refines the GREEN step
- [Impasses in TDD](impasses-in-tdd.md) — what TPP helps you avoid
- [Simple Design](simple-design.md) — TPP is "fewest elements" applied to transformations
- [Programming by Wishful Thinking](programming-by-wishful-thinking.md) — complementary tool for the design side
