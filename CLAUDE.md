# CLAUDE.md — Teaching the SOLID Book

## Project Purpose

Teaching the user the SOLID book ("SOLID: An Ontology of Software Design") chapter by chapter, saving each lesson as a markdown file with mermaid diagrams for retention.

## Source Material

- Parsed EPUB output lives in `/output/` organized by Parts and Chapters
- Always read the source chapter before writing the teaching file

## Output Structure

```
teaching/
├── part-ii-humans-and-code/
│   ├── 01-demystifying-clean-code.md
│   ├── 02-human-centered-design.md
│   └── ...
├── part-iii-.../
│   └── ...
└── concepts/
    ├── simple-design.md
    ├── tdd.md
    └── ...
```

- One teaching file per chapter, numbered to match book order
- Folder per Part, named to match the book's part titles
- `concepts/` is flat — one file per concept, shared across all chapters

## Teaching File Format

Each chapter teaching file follows this structure:

1. **Title** — `# Chapter N: Name`
2. **Core Question** — one bold question the chapter answers
3. **Numbered sections** — walk through the chapter's ideas in order, each with:
   - Clear explanation in plain language
   - Tables for comparisons (community vs expert, before vs after, etc.)
   - Code examples where relevant (keep them short)
   - Blockquotes for key quotes from the book
4. **Mermaid diagrams** — for flows, comparisons, and the final mental map
5. **Key Takeaways** — numbered list, bold the main point of each
6. **Concepts Introduced** — linked list to concept files

## Concept Files

Each concept file covers:

1. **Origin** — who coined it, when
2. **What It Is** — plain language definition
3. **Comparison table** — if there's a natural contrast (e.g., emergent vs BDUF)
4. **Examples** — concrete, not abstract
5. **The Key Insight** — one sentence that sticks
6. **Related** — links to other concept files

Concept files are created when a concept is first introduced. If a later chapter deepens the concept, update the existing file rather than creating a new one.

## Mermaid Diagram Rules

- One label per node — never use `\n`, `<br/>`, or any line break inside a node label
- If a node needs sub-info, split into parent + child nodes connected by arrows
- Use `-.->` (dotted) for annotations/details, `-->` (solid) for main flow
- Use `style` for color coding: `#d9ead3` green for good, `#f4cccc` red for bad
- Use subgraphs for side-by-side comparisons (e.g., bad vs good patterns)
- Use `~~~` (invisible link) to control layout between subgraphs
- Keep diagrams simple — fewer nodes is better than comprehensive nodes
- Every chapter teaching file should end with a mental map flowchart summarizing the full chapter

## Writing Style

- Teach, don't summarize — explain *why* things matter, not just what they are
- Use the author's own examples and quotes where they're good
- Add your own analogies only when they genuinely clarify
- Be direct — no filler, no "let's dive in", no "as we discussed"
- Use tables heavily — they compress information well
- Bold key terms on first introduction
- Use `>` blockquotes for book quotes and key definitions

## Workflow

1. Read the source chapter from `/output/`
2. Teach the user in conversation (interactive, can answer questions)
3. Save the teaching file to the appropriate `teaching/` subfolder
4. Create concept files for any newly introduced concepts in `teaching/concepts/`
5. If a concept already has a file, update it with new information from the current chapter rather than duplicating
