---
paths:
  - "**/*.cs"
---

# C# Conventions

## Formatting

- Apply code-formatting style defined in `.editorconfig`
- Prefer file-scoped namespace declarations and single-line using directives

## Nullable Reference Types

- Declare variables non-nullable, and check for `null` at entry points
- Always use `is null` or `is not null` instead of `== null` or `!= null`
- Trust the C# null annotations — never add null checks when the type system guarantees a value cannot be null
- Never suppress nullable warnings with `!` unless accompanied by an explanatory comment

## Code Style

- Prefer `sealed record` over classes for immutable DTOs and value objects
- Async all the way: never block with `.Result` or `.Wait()`
- Suffix all methods returning `Task` or `Task<T>` with `Async` — except overrides or interface implementations where the name is imposed
- Always propagate `CancellationToken` through async call chains — never ignore it
- Use `ILogger<T>` for logging, never `Console.WriteLine`
