# Leaky Abstractions

**Origin**: Joel Spolsky, "The Law of Leaky Abstractions" (2002)

## What It Is

An abstraction **leaks** when you need to understand its internal implementation details to use it correctly. The whole point of an abstraction is to hide complexity — when it leaks, it fails at its job.

## The Book's Example: HTTPService

```typescript
// ❌ Leaky: must know to call initialize() before using
class HTTPService {
  http: AxiosInstance;
  initialize(baseURL: string) {
    this.http = axios.create({ baseURL });
  }
}

// Developer does:
const service = new UserService();
service.getUsers(); // 💥 CRASH — http not initialized
```

The abstraction leaks because you must know about `initialize()` — an internal detail — to avoid errors.

```typescript
// ✅ Fixed: constructor enforces correct setup
class HTTPService {
  http: AxiosInstance;
  constructor(baseURL: string) {
    this.http = axios.create({ baseURL });
  }
}

// Developer does:
const service = new UserService("http://api.com");
service.getUsers(); // ✅ works
```

## The Principle

> **Avoid partial object creation** — ensure the object is fully created or not created at all.

Use language constructs (constructors, factory methods, type systems) to make the wrong thing impossible, not just discouraged.

## How to Spot Leaks

- "You have to call X before Y" (temporal coupling)
- "Make sure you set this flag or it won't work" (hidden precondition)
- "It works, but only if you pass the right type of..." (insufficient type safety)
- Error messages that expose internal implementation

## Related

- [Developer Experience](./developer-experience.md) — leaky abstractions are DX failures
- [Coupling & Cohesion](./coupling-and-cohesion.md) — leaks create coupling to internals
