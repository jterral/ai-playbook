---
name: dotnet-check
description: Build a C#/.NET project and run its unit tests. Use when the user asks to build, check, or verify a .NET solution or run dotnet tests.
---

## Prerequisites

- **.NET SDK**: .NET 6+ must be installed (`dotnet` command available)
- **Project structure**: Must have a `.sln` or `.csproj` file in the root or working directory
- **Unit tests**: UnitTests project must exist and follow naming convention `*UnitTests`
- **Dependencies**: All NuGet dependencies must be restorable

## Steps

1. Run `dotnet build`
2. If build fails, stop and report errors clearly
3. Run `dotnet test --filter "FullyQualifiedName~UnitTests"`
4. Report results summary
