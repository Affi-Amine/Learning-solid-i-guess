# Refactoring Recipes

## Origin

The recipe format comes from **Martin Fowler**'s *Refactoring* (1999, 2nd ed. 2018). Each refactoring has: a name, a motivation, a mechanics section (step-by-step), and an example. **refactoring.guru** mirrors this catalog online.

## What They Are

**Step-by-step transformations** that change the structure of code without changing its behavior. Tests stay green throughout.

```
For every code smell, there's at least one refactoring that addresses it.
```

## The Smell → Refactoring Map

### Bloaters

| Smell | Refactoring |
|---|---|
| Long Method | Extract Method, Decompose Conditional |
| Large Class | Extract Class, Extract Subclass |
| Long Parameter List | Introduce Parameter Object, Replace Parameter with Method Call |
| Data Clumps | Extract Class, Introduce Parameter Object |
| Primitive Obsession | Replace Data Value with Object, Replace Type Code with Class |

### OO Abusers

| Smell | Refactoring |
|---|---|
| Switch Statements | Replace Conditional with Polymorphism, Replace Type Code with Subclasses |
| Refused Bequest | Push Down Method/Field, Replace Inheritance with Delegation |
| Temporary Field | Extract Class, Introduce Null Object |
| Alternative Classes | Rename Method, Move Method, Extract Superclass |

### Change Preventers

| Smell | Refactoring |
|---|---|
| Shotgun Surgery | Move Method, Move Field, Inline Class |
| Divergent Change | Extract Class |
| Parallel Inheritance | Move Method, Move Field |

### Dispensables

| Smell | Refactoring |
|---|---|
| Dead Code | Delete it |
| Lazy Class | Inline Class, Collapse Hierarchy |
| Data Class | Encapsulate Field, Move Method |
| Duplicate Code | Extract Method, Pull Up Method, Form Template Method |
| Comments (poor) | Extract Method, Rename Variable, Replace Comment with Function |
| Speculative Generality | Collapse Hierarchy, Inline Class, Remove Parameter |

### Couplers

| Smell | Refactoring |
|---|---|
| Feature Envy | Move Method, Extract Method |
| Inappropriate Intimacy | Move Method/Field, Hide Delegate, Change Bidirectional to Unidirectional Association |
| Message Chains | Hide Delegate, Extract Method |
| Middle Man | Remove Middle Man, Inline Method |

## The Standard Recipe

Each refactoring follows the same shape:

1. **Identify** the smell
2. **Add tests** if not already covered
3. **Apply the recipe** in tiny steps, running tests between each
4. **Verify** behavior unchanged
5. **Commit**

## Worked Example: Replace Conditional with Polymorphism

### Before
```typescript
class Bird {
  constructor(public type: 'european' | 'african' | 'norwegianBlue') {}

  speed(): number {
    switch (this.type) {
      case 'european': return 35;
      case 'african': return 40;
      case 'norwegianBlue': return 0;
    }
  }
}
```

### Recipe Steps
1. Make `Bird` abstract
2. Create subclass for each type
3. Move the body of each `case` into its own subclass
4. Remove the `switch`

### After
```typescript
abstract class Bird {
  abstract speed(): number;
}

class EuropeanBird extends Bird {
  speed() { return 35; }
}

class AfricanBird extends Bird {
  speed() { return 40; }
}

class NorwegianBlue extends Bird {
  speed() { return 0; }
}
```

Tests still pass. Adding a new bird = new class, no edits to existing code.

## How To Get Good At This

| Practice | Benefit |
|---|---|
| Memorize the Top 7 smells | Covers 80% of cases |
| Bookmark refactoring.guru | Quick reference |
| Pair with someone fluent | Watch the moves |
| Refactor in tiny steps | Tests always green |
| Commit after each refactoring | Easy revert |

## The Key Insight

**Refactoring is mechanical, not creative.** Once you've identified the smell, the recipe tells you the moves. The skill is in detection, not invention.

## Related

- [Code Smells](code-smells.md) — what triggers a refactoring
- [Code Smell Categories](code-smell-categories.md) — how to triage smells
- [Object Calisthenics](object-calisthenics.md) — prevention vs cure
- [TDD](tdd.md) — refactoring is the third step of red-green-refactor
- [Anti-Patterns](anti-patterns.md) — when refactoring isn't enough; rework needed
