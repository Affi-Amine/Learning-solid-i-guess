# Conceptual Models

**Origin**: Don Norman, "The Design of Everyday Things"

## What It Is

A **conceptual model** is a high-level mental explanation of how something works. It's imperfect, skips details, but it's *good enough* to let you use the thing effectively and predict the effects of your actions.

## Examples


| Thing              | Full Truth                                        | Good Enough Conceptual Model                         |
| ------------------ | ------------------------------------------------- | ---------------------------------------------------- |
| Elevators          | Complex machinery, counterweights, safety systems | Press button, doors open, press floor, it goes there |
| The Cloud          | AWS EC2, databases, networking, replication       | "My files are stored somewhere on the internet"      |
| React              | Virtual DOM, reconciliation, fiber architecture   | "It re-renders when state changes"                   |
| Repository Pattern | Query builders, connection pools, transactions    | "It knows how to store and retrieve my objects"      |


## Why It Matters

Without a conceptual model, you're **guessing**. You try random things and hope they work. With one, you can predict what will happen before you act.

In code: if a new developer can quickly build a correct conceptual model of your codebase, they become productive fast. If they can't, every task is trial and error.

## How Conceptual Models Get Built

All the other HCD principles feed into building the conceptual model:

- **Affordances** show what's possible
- **Signifiers** show where and how
- **Constraints** narrow the options
- **Mapping** shows the relationships
- **Feedback** confirms or corrects after action

The conceptual model is the **end product** of good design.

## In Code

- **Design patterns** are named conceptual models (Factory = "creates objects", Observer = "notifies on change")
- **Encapsulation** lets you work with a simplified model without knowing internals
- **BDD tests** build the conceptual model by describing behavior in plain language

## Related

- [Human-Centered Design](./human-centered-design.md)
- [HCD Principles](./hcd-principles.md)

