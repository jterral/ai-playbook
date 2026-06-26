---
paths:
  - "src/**/*.cs"
---

# C# Conventions - Source

## Architecture

- Strict Clean Architecture: no business logic in controllers
  - Controllers should only: validate input, call a service, and return a response
