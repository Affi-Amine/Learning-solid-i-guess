# Event Storming

**Origin**: Alberto Brandolini (2013), improvised when short on time for a UML session

## What It Is

An interactive workshop where developers and domain experts use **sticky notes on a wall** to map out the entire business domain chronologically. The goal: build a shared mental model before writing any code.

## How It Works

1. Gather domain experts, developers, stakeholders in one room with lots of wall space
2. Everyone writes **domain events** (past tense, orange stickies) and places them on the wall
3. Sort events **chronologically**, left to right. Stack alternatives vertically.
4. Identify **commands** (imperative, blue stickies) that cause each event
5. Optionally identify **aggregates** (yellow stickies) between command-event pairs
6. Draw circles around groups to identify **subdomains**
7. Mark **problem areas** (red stickies) for things that need more investigation

## Key Techniques

- **Push to the edges**: ask "what happens before the first event?" and "what happens after the last?" to find hidden requirements
- **System events**: some events are generated automatically (e.g., `SubscriptionExpired` after 30 days)
- **Sad paths**: commands can fail — note failure reasons but save details for acceptance tests later

## What You Get

At the end of a session:
- A timeline of the entire business process
- All commands (features) identified
- Subdomains named and bounded
- A shared vocabulary (ubiquitous language)
- Problem areas flagged for investigation

## Event Storming vs Event Modelling

| | Event Storming | Event Modelling |
|---|---|---|
| UI/queries | Hard to discover | Rough UI sketches included |
| Cross-subdomain flows | Messy on linear timeline | Swimlanes per subdomain |
| Best for | Initial domain discovery | Detailed system design |

## Related

- [Domain Events](./domain-events.md) — the building blocks plotted in Event Storming
- [DDD](./ddd.md) — Event Storming is a core DDD practice
- [Subdomains](./subdomains.md) — discovered through Event Storming
