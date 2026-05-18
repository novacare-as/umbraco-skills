# Middleware Ordering | AI in Umbraco

Control the execution order of middleware in the pipeline.

Understanding Order

```
Registration order: A, B, C

Result: C wraps (B wraps (A wraps Client))

Execution flow:
  Request  → C → B → A → Client → Response
  Response ← C ← B ← A ← Client ←
```

Builder Methods

| Method | Description |
|---|---|
| `Append<T>()` | Add middleware at the end |
| `InsertBefore<TBefore, T>()` | Insert before a specific middleware |
| `InsertAfter<TAfter, T>()` | Insert after a specific middleware |
| `Remove<T>()` | Remove a middleware |

Basic Ordering

Inserting Relative to Others

Removing Middleware

Embedding Middleware Ordering

Common Patterns

Multiple Composers

Last updated

Was this helpful?