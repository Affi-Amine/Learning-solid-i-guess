# Control Styles

## Origin

Described in **Rebecca Wirfs-Brock**'s *Object Design* (2002). A way to characterize how decision-making and orchestration flow through an OO system.

## What They Are

Three patterns for how control passes between objects:

| Style | Description |
|---|---|
| **Centralized** | One object knows almost everything and tells others what to do |
| **Delegated** | A coordinator orchestrates, but each helper handles its own logic |
| **Dispersed** | No central authority; objects react to events independently |

## Comparison

| Aspect | Centralized | Delegated | Dispersed |
|---|---|---|---|
| **Coordinator** | One big one | Thin orchestrator | None |
| **Knowledge spread** | Concentrated | Balanced | Scattered |
| **Easy to follow flow?** | Yes | Yes | Hard |
| **Easy to extend?** | No (god class) | Yes | Yes (if events well-named) |
| **Best for** | Simple scripts, prototypes | Most apps | Event-driven systems, games |

## Examples

### Centralized

```typescript
class GameController {
  movePiece(id, to) {
    // Knows board layout, validation rules, logging format,
    // turn rules, win conditions — all in one method.
    if (this.board[to.x][to.y]) { /* ... */ }
    if (this.pieces[id].color !== this.turn) { /* ... */ }
    // ... 200 lines
  }
}
```

Easy to write at first. Becomes a god class. Hard to test.

### Delegated

```typescript
class Game {
  constructor(
    private board: Board,
    private validator: MoveValidator,
    private logger: Logger
  ) {}

  movePiece(id, to) {
    if (!this.validator.isMoveValid(this.board, id, to)) return;
    this.board.executeMove(id, to);
    this.logger.record(...);
    this.switchTurn();
  }
}
```

Each helper owns its logic. The coordinator just orchestrates.

### Dispersed

```typescript
eventBus.on('PIECE_MOVED', (e) => board.update(e));
eventBus.on('PIECE_MOVED', (e) => logger.record(e));
eventBus.on('PIECE_MOVED', (e) => turnManager.advance());

// UI emits the event:
ui.onDrop = (id, to) => eventBus.emit('PIECE_MOVED', { id, to });
```

No central controller. Powerful but harder to follow — you have to grep for event listeners.

## Choosing a Style

| Situation | Pick |
|---|---|
| Quick script or kata | Centralized — fastest to write |
| Web/mobile app, business logic | Delegated — best general fit |
| Many concurrent agents, plugins, async pipelines | Dispersed — events scale better |
| Game with many independent objects (NPCs, particles) | Dispersed |
| Domain-heavy, transactional system | Delegated (with maybe domain events for some flows) |

## The Key Insight

**Control style is a design decision, not an accident.** Pick it consciously. Most systems benefit from **delegated** with selective use of events for cross-cutting concerns.

## Related

- [Responsibility-Driven Design](responsibility-driven-design.md) — the parent process where you choose this
- [Object Stereotypes](object-stereotypes.md) — Coordinators and Controllers are the central pieces in delegated style
- [Coupling and Cohesion](coupling-and-cohesion.md) — control style directly affects both
- [Domain Events](domain-events.md) — the building block for dispersed style
