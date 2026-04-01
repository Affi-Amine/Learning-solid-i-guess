# The Either Pattern

**Origin**: Functional programming (Haskell, Scala). Adapted for TypeScript by various authors.

## What It Is

A typed container that holds **either** a success value or a failure value — never both. It replaces returning `null`, throwing exceptions, or using untyped error strings.

```typescript
type Either<S, F> = Success<S, F> | Failure<S, F>;
```

## Why It Exists

Traditional error handling has problems:

| Approach | Problem |
|---|---|
| Return `null` | Doesn't say *which* error. Forces null-checks everywhere. |
| Throw errors | Disrupts flow. Error messages are fragile strings. Not typed. |
| Error codes | Easy to forget to check. Not self-documenting. |

The Either pattern fixes all three: errors are **typed**, **visible in the signature**, and **don't disrupt flow**.

## How It Works

```typescript
// Define the result type — ALL outcomes are visible
type CreateUserResult = Either<
  CreateUserSuccess,
  EmailInvalid | UserAlreadyExists | PasswordDoesntMeetCriteria
>;

// Return success or failure
function createUser(req): CreateUserResult {
  if (!isEmailValid()) return failure(new EmailInvalid(req.email));
  return success(new CreateUserSuccess(user.id));
}

// Consumer — check which one you got
const result = createUser(req);
if (result.isSuccess()) { /* use result.value */ }
if (result.isFailure()) { /* handle typed error */ }
```

## Key Properties

- **Errors are typed classes** — encapsulate message construction, switch on `constructor`
- **All outcomes visible** — the return type documents every possible failure
- **No surprises** — consumer knows upfront what can go wrong
- **No flow disruption** — `return failure(...)` instead of `throw`

## Errors vs. Exceptions

The Either pattern handles **errors** (expected, domain-level). For **exceptions** (unexpected, I/O failures), wrap in try/catch and convert to a typed error:

```typescript
try {
  user = db.save(data);
} catch (err) {
  return failure(new DatabaseError(err));
}
```

## Related

- [Value Objects](./value-objects.md) — factory methods can return Either instead of throwing
- [CQS](./cqs.md) — commands return Either to signal success/failure
- [HCD Principles](./hcd-principles.md) — typed errors are constraints and feedback
- [Accidental vs Essential Complexity](./accidental-vs-essential-complexity.md) — errors are essential, exceptions are accidental
