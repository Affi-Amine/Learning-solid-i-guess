# Learning SOLID (I Guess)

A structured, chapter-by-chapter study of **"SOLID: An Ontology of Software Design"** by Khalil Stemmler.

## About the Book

SOLID is not just another "clean code" book. It's a comprehensive ontology of software design that bridges the gap between theory and practice. It covers:

- **Human-Centered Design** applied to code — using Don Norman's design principles to write code that humans can actually understand
- **Test-Driven Development** as the engine that drives design, not just a testing strategy
- **Object-Oriented Design** with a focus on coupling, cohesion, and the SOLID principles
- **Design Patterns** used as tools, not dogma
- **Domain-Driven Design** for modeling complex business logic
- **Architecture** — from clean architecture to feature-driven structure

The book's core thesis: software design is the tension between **structure** (correctness, maintainability) and **developer experience** (discoverability, understandability). Great design finds the Aristotelian mean between the two.

## What This Repo Is

This is my personal learning repo. Each chapter gets broken down into a teaching file that distills the key ideas, with:

- Clear explanations in plain language
- Tables for comparisons and quick reference
- Mermaid diagrams for mental maps and retention
- Code examples where they help
- Key takeaways at the end of each chapter

Every new concept introduced (TDD, DDD, coupling, cohesion, etc.) also gets its own standalone reference file in the `concepts/` folder, building up a personal knowledge base over time.

## Repo Structure

```
teaching/
  part-ii-humans-and-code/       # Part II: Humans & Code
    01-demystifying-clean-code.md
    02-human-centered-design-for-developers.md
    03-organizing-things.md
    04-documentation-and-repositories.md
    05-naming-things.md
    06-comments.md
    ...
  part-iii-.../                   # Future parts
    ...
  concepts/                       # Standalone concept reference files
    simple-design.md
    tdd.md
    coupling-and-cohesion.md
    ddd.md
    ...
```

- **Chapter files** walk through each chapter's ideas in order, with diagrams and takeaways
- **Concept files** are deeper dives into individual concepts, cross-linked across chapters
- As later chapters deepen a concept, the existing concept file gets updated rather than duplicated

## Progress

- [ ] Part I: Foundations
- [x] Part II: Humans & Code (Chapters 4-9, in progress)
- [ ] Part III: Phronesis
- [ ] Part IV: Test-Driven Development Basics
- [ ] Part V: Object-Oriented Design With Tests
- [ ] Part VI: Design Patterns
- [ ] Part VII: Design Principles
- [ ] Part VIII: Architecture Essentials
- [ ] Part IX: Advanced Object-Oriented Design
- [ ] Part X: Advanced Test-Driven Development

