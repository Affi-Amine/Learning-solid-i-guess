# Programming by Wishful Thinking

## Origin

Coined in *Structure and Interpretation of Computer Programs* (Abelson & Sussman, 1985). Popularized in TDD circles as a way to design APIs by using them before they exist.

## What It Is

Write the code that *uses* a function or object as if it already worked, then build the implementation to match. You design the interface from the caller's perspective.

In TDD, this happens naturally when you write the assertion first — you reach for the API you *wish* existed.

## Comparison

| Bottom-Up (Conventional) | Wishful Thinking (Top-Down) |
|---|---|
| Build the implementation first | Write the calling code first |
| Risk inventing abstractions you don't need | Only build what the caller actually uses |
| Imperative, step-by-step thinking | Declarative — describe what you want |
| API shaped by implementation constraints | API shaped by usage |

## Examples

### In a Unit Test (Backwards AAA)

```typescript
// Assert — invent the method that proves correctness
expect(game.getCurrentTurn()).toBe('O');

// Act — invent the simplest call that triggers it
game.chooseMark({ row: 0, column: 0 });

// Arrange — invent the constructor
let game = new Game();
```

Three methods designed (`new Game()`, `chooseMark`, `getCurrentTurn`) without writing a line of production code.

### In an Acceptance Test (Walking Skeleton)

```typescript
Given("I'm on the map page", () => {
  mapPage.load();
})

Then("at least one spot should be displayed", () => {
  mapPage.getCurrentStudySpotsInViewOnMap()
    .should('have.length.greaterThan', 0)
})
```

`mapPage` doesn't exist yet. The Page Object's interface is being designed by the test.

### In Production Code (Sketching)

```typescript
function processOrder(order: Order) {
  const validated = validate(order);          // doesn't exist yet
  const priced = applyPricing(validated);     // doesn't exist yet
  const stored = repository.save(priced);     // doesn't exist yet
  return notify(stored);                      // doesn't exist yet
}
```

Read the function and the design is obvious. Now go fill in each helper.

## When to Use It

| Situation | Why It Helps |
|---|---|
| Stuck on how to verify a behavior | Forces you to imagine success first |
| Designing a public API | Caller's perspective produces ergonomic interfaces |
| Acceptance tests / E2E tests | Page Objects emerge from how tests want to use them |
| Sketching a feature top-down | Names and signatures emerge before details |

## The Key Insight

**Design from the call site, not the implementation site.** What the caller wishes for is almost always cleaner than what the implementer would invent bottom-up.

## Related

- [TDD](tdd.md) — wishful thinking is a core TDD design move
- [Acceptance Tests](acceptance-tests.md) — Given-When-Then is wishful thinking applied to user stories
- [Walking Skeleton](walking-skeleton.md) — the failing E2E test is wishful thinking at the system level
- [Simple Design](simple-design.md) — wishful thinking helps you avoid premature abstraction
