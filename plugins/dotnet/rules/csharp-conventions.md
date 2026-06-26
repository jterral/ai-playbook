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
