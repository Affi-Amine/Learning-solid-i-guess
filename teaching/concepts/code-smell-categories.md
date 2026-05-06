# Code Smell Categories

## Origin

Categorization popularized by **refactoring.guru** based on Martin Fowler's *Refactoring* (1999, 2nd ed. 2018). Groups smells by what causes them, making detection systematic.

## The Five Categories

| Category | Theme | "If I see…" Question |
|---|---|---|
| **Bloaters** | Things grown too large | "Is this method/class/parameter list out of control?" |
| **OO Abusers** | Misused OO features | "Is this procedural code dressed as OO?" |
| **Change Preventers** | Code resists modification | "Why does one change require so many edits?" |
| **Dispensables** | Code earns nothing | "Could I delete this without losing anything?" |
| **Couplers** | Inappropriate dependencies | "Why does this class know so much about that class?" |

## 1. Bloaters

Things that grow until they're unwieldy.

| Smell | What It Looks Like |
|---|---|
| **Long Method** | A method spans screens; hard to scan |
| **Large Class** | A class with many fields and many methods |
| **Long Parameter List** | More than ~3 parameters |
| **Data Clumps** | Same group of fields/parameters appearing together repeatedly |
| **Primitive Obsession** | Primitives carrying domain meaning |

## 2. Object-Orientation Abusers

OO features misused or avoided.

| Smell | What It Looks Like |
|---|---|
| **Switch Statements** | Branching on type instead of polymorphism |
| **Refused Bequest** | Subclass uses few methods of its parent |
| **Temporary Field** | Fields used only some of the time |
| **Alternative Classes with Different Interfaces** | Two classes do the same thing with different APIs |

## 3. Change Preventers

One change rippling everywhere — or one class changing for many reasons.

| Smell | What It Looks Like |
|---|---|
| **Shotgun Surgery** | One change → edits in many files |
| **Divergent Change** | One class edited for unrelated reasons |
| **Parallel Inheritance Hierarchies** | Adding to one hierarchy forces additions in another |

## 4. Dispensables

Code that doesn't earn its keep.

| Smell | What It Looks Like |
|---|---|
| **Comments** (poor) | Comments that re-explain the code instead of clarifying intent |
| **Duplicate Code** | Same logic in multiple places |
| **Lazy Class** | A class barely doing anything |
| **Data Class** | A class that's just fields and getters/setters |
| **Dead Code** | Unused parameters, methods, classes |
| **Speculative Generality** | Abstractions for hypothetical future needs |

## 5. Couplers

Excessive intimacy between classes.

| Smell | What It Looks Like |
|---|---|
| **Feature Envy** | A method uses another class's data more than its own |
| **Inappropriate Intimacy** | One class accesses another's internals |
| **Message Chains** | `a.b().c().d().e()` |
| **Middle Man** | A class that just delegates with no added value |

## How To Use Categories

1. When code feels off, run through the five categories
2. Ask each category's diagnostic question
3. The first "yes" tells you which catalog of refactorings to consult

| Category | Common Refactorings |
|---|---|
| **Bloaters** | Extract Method, Extract Class, Introduce Parameter Object, Replace with Value Object |
| **OO Abusers** | Replace Conditional with Polymorphism, Replace Type Code with Subclasses |
| **Change Preventers** | Move Method, Move Field, Inline Class |
| **Dispensables** | Remove Dead Code, Inline Class, Collapse Hierarchy, Replace Comment with Function |
| **Couplers** | Hide Delegate, Move Method, Extract Class |

## The Key Insight

**Categories make detection systematic.** Without them, "this code feels bad" is vague. With them, "this is a Coupler — specifically Feature Envy" points directly at the fix.

## Related

- [Code Smells](code-smells.md) — the parent topic
- [Anti-Patterns](anti-patterns.md) — larger-scale problems
- [Refactoring Recipes](refactoring-recipes.md) — the smell-to-fix mapping
- [Object Calisthenics](object-calisthenics.md) — prevention via constraint
- [Object Stereotypes](object-stereotypes.md) — clarifies which class should hold which responsibility
