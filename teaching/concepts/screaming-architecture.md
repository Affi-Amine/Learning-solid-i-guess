# Screaming Architecture

**Origin**: Robert C. Martin (Uncle Bob), 2011 blog post

## What It Is

Your project's folder structure should **scream** the use cases of the application, not the framework or infrastructure it's built with.

## The Test

Open your project root. What does it tell you?

| Infrastructure-Driven (Bad) | Feature-Driven (Good) |
|---|---|
| `components/`, `hooks/`, `services/`, `utils/` | `checkout/`, `userProfile/`, `dashboard/` |
| "This is a React app" | "This is an e-commerce app" |
| You know the tech stack | You know what the system *does* |

## Why It Matters

- **New developers** can understand the system's capabilities in seconds
- **Locating features** becomes trivial — the folder name matches the feature name
- **Adding features** is obvious — create a new feature folder
- **Removing features** is clean — delete the folder

## The Quote

> "Software architectures are structures that support the use cases of the system. Just as the plans for a house or a library scream about the use cases of those buildings, so should the architecture of a software application scream about the use cases of the application." — Robert C. Martin

## Related

- [Feature-Driven Structure](./feature-driven-structure.md) — the practical implementation
- [Coding Standards](./coding-standards.md) — screaming architecture is a structural coding standard
- [HCD Principles](./hcd-principles.md) — folder names are signifiers; feature folders improve discoverability
