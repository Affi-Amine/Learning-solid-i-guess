# Developer Experience (DX)

## What It Is

Where UX designs for end users, **DX designs for developers**. It applies to APIs, tools, languages, frameworks, and — critically — **your own codebase**.

## The Key Questions

**Getting started:**
- How do I run this locally?
- How do I debug it?

**Being productive:**
- What are all the things I can do?
- How easy is it to understand what this code does?
- How quickly can I find what to change?
- What was the learning curve like?

## DX vs. Structure

This is the **central tension** of software design:

- More structure → higher learning curve → worse initial DX
- More freedom → easier start → worse DX at scale (chaos)

The goal is the **Aristotelian mean**: enough structure to maintain quality, enough freedom to stay productive.

## Examples

| Good DX (balanced) | Poor DX |
|---|---|
| React + TypeScript | Untyped React at scale |
| Clear error messages | Stack traces with no context |
| Consistent patterns | Every file structured differently |
| Constructor enforces setup | Must call `initialize()` before use |

## Why It Matters for Everyone

You don't need to work at Stripe or GitHub for DX to matter. If your code will ever be read or used by another developer (including future you), you're an API designer. Your abstractions, naming choices, and structural decisions **are** the developer experience.

## Related

- [Coding Standards](./coding-standards.md) — standards create consistent DX
- [Leaky Abstractions](./leaky-abstractions.md) — leaks are DX failures
