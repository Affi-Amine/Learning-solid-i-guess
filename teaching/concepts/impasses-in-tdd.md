# Impasses in TDD

## Origin

Discussed by Kent Beck (*TDD by Example*) and Uncle Bob's writings on the Transformation Priority Premise. The term **impasse** (also: deadlock) describes a TDD trap where the next test can't be added without rewriting most of the existing code.

## What It Is

A situation where:

- A new failing test can't be made to pass
- Without **ripping apart and rewriting** the code that already passes earlier tests

You've painted yourself into a corner. The only safe escape is reverting to the last green commit and choosing a different path.

## How Impasses Happen

| Cause | Symptom |
|---|---|
| **Jumped to a complex transformation early** | Reached for a design pattern in test 2 |
| **Coupled to an arbitrary implementation choice** | Fake-it value baked into the structure |
| **Premature abstraction** | Built a framework when a constant would have done |
| **Wrong data structure** | Picked an array when you needed a map; restructure breaks all tests |

## Recognizing One

You're approaching an impasse when:

- The "simplest thing that could work" feels elaborate
- You're modifying 3+ existing tests to keep them green
- You're tempted to delete tests rather than evolve the code
- Each new test forces a redesign of the previous code

## Escape Plan

```
1. Stop.
2. Revert to the last green commit.
3. Pick a transformation higher on the TPP list.
4. Re-add the tests one by one with the new approach.
```

The cost of reverting is small — usually a few minutes. The cost of pushing through an impasse is hours of broken tests and shaky design.

## Prevention

| Tactic | How |
|---|---|
| **Use TPP** | Always pick the highest-priority transformation that works |
| **Triangulate gradually** | Don't generalize off one example |
| **Rule of Three** | Don't extract abstractions until duplication appears 3 times |
| **Fake It longer** | If unsure, hardcode for now and let later tests force the generalization |
| **Commit on green** | Every passing test is a checkpoint |

## Examples

### Impasse-prone

```typescript
// Test 1: returns "Fizz" for 3.
// Jump to a Strategy pattern with FizzRule, BuzzRule, FizzBuzzRule classes.

// Test 2: validates input range.
// Now the whole strategy class hierarchy doesn't fit the new constraint.
// Forced to rewrite.
```

### Impasse-resistant

```typescript
// Test 1: returns "Fizz" for 3.        →  return "Fizz";    (constant)
// Test 2: returns "Buzz" for 5.        →  if/else            (conditional)
// Test 3: returns "FizzBuzz" for 15.   →  add a branch       (still conditional)
// Test 4: validates input range.       →  add a guard        (still conditional)
// ...refactor to strategy only when patterns appear 3+ times.
```

## The Key Insight

**An impasse means you committed to design too early.** The fix is humility: revert, take smaller steps, let the tests force the design rather than imposing it.

## Related

- [TDD](tdd.md) — impasses are a failure mode to actively avoid
- [Transformation Priority Premise](transformation-priority-premise.md) — the main tool for prevention
- [Simple Design](simple-design.md) — Rule of Three keeps abstractions honest
- [Emergent Design](emergent-design.md) — design that emerges from tests resists impasses
