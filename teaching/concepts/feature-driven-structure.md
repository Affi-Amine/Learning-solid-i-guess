# Feature-Driven Structure

## What It Is

Organizing your project folders around **features/use cases** rather than technical infrastructure. Every file either belongs to a specific feature folder or to a shared infrastructure folder.

## The Two Buckets Rule

```
Does this code belong to a specific feature?
  Yes → put it in the feature folder
  No  → put it in /shared
```

No third option. This eliminates "where does this go?" permanently.

## Backend Structure

```
src/
  modules/
    users/
      useCases/
        createUser/
          CreateUserUseCase.ts
          CreateUserController.ts
          CreateUserErrors.ts
          createUser.spec.ts
        deleteUser/
  shared/
    core/
    infra/
    utils/
```

Each use case folder is a self-contained workspace.

## Frontend Structure

Features live in **pages** (the top-level component rendered per route):

```
src/
  pages/
    checkout/
      checkout.page.ts
      checkout.spec.ts
      components/
      useCases/
        placeOrder.ts
  shared/
    components/
    infra/
```

Pages have a 1-to-many relationship with features.

## Rules

| Rule | Why |
|---|---|
| Co-locate tests with code | No duplicate folder trees to maintain |
| Fight the framework | Tuck framework code in `shared/infra/`, keep your structure |
| Follow top-level conventions | `src/`, `dist/`, `public/` |
| Feature folders = workspaces | All code for one feature in one place |

## Benefits

- Features are discoverable from the folder names
- Reduced file-flipping (everything for a feature is co-located)
- Coupling becomes visible (if you flip between feature folders, there's a coupling problem)
- Easy to test, add, change, and remove features

## Related

- [Screaming Architecture](./screaming-architecture.md) — the philosophy behind it
- [Coupling & Cohesion](./coupling-and-cohesion.md) — feature folders enforce high cohesion
- [Human-Centered Design](./human-centered-design.md) — feature folders are signifiers that improve discoverability
