---
paths:
  - "src/**/*.cs"
---

# C# Conventions - Source

## Architecture

- Strict Clean Architecture: no business logic in controllers
  - Controllers should only: validate input, call a service, and return a response

## Naming

- Use Async suffix for async methods, except for overrides or interface implementations where the name is imposed

## Code Style

- Prefer `sealed record` over classes for immutable DTOs and value objects
- Async all the way: never block with `.Result` or `.Wait()`
- Suffix all methods returning `Task` or `Task<T>` with `Async` — except overrides or interface implementations where the name is imposed
- Always propagate `CancellationToken` through async call chains — never ignore it
- Use `ILogger<T>` for logging, never `Console.WriteLine`

## ❌ Don'ts

### Frameworks

- **Do not use MediatR** — prefer direct service injection. The library went commercial, and MediatR adds indirection without benefit at our scale and makes call chains harder to trace.
- **Do not use AutoMapper** — prefer explicit mapping. AutoMapper adds indirection and makes call chains harder to trace.
- **Do not use FluentAssertions** — prefer explicit assertions. FluentAssertions went commercial.

### Repositories

- **Do not put business logic in repositories** — repositories are data-access only.
