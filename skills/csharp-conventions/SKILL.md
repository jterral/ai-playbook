---
name: csharp-conventions
description: C# and .NET coding conventions. Use automatically when working on C# or .NET code, implementing features, adding dependencies, reviewing existing C# code, or writing tests in a C# project.
user-invocable: false
tools: [read, write]
---

# C# Conventions

## Architecture

- Strict Clean Architecture: no business logic in controllers
  - Controllers should only: validate input, call a service/mediator, and return a response
- Prefer `sealed record` over classes for immutable DTOs and value objects

## Code Style

- Async all the way: never block with `.Result` or `.Wait()`
- Suffix all methods returning `Task` or `Task<T>` with `Async` — except overrides or interface implementations where the name is imposed (e.g. MediatR `Handle`)
- Always propagate `CancellationToken` through async call chains — never ignore it
- Use `ILogger<T>` for logging, never `Console.WriteLine`
- Enable and respect nullable reference types — never suppress warnings with `!` unless accompanied by an explanatory comment

## Unit Testing

- Use `xUnit` for unit tests
- Use `Moq` for mocking dependencies
- Use `sealed` test classes to prevent inheritance and ensure test isolation
- Follow the Arrange-Act-Assert pattern in tests, _ALWAYS_ add comments to separate the sections
- Use a private readonly field named `_sut` for the System Under Test
- Use private readonly fields suffixed with `Mock` for mocked dependencies, e.g. `_flipClientMock`
- Always initialize mocks inline with `new Mock<T>()`
- Always initialize `_sut` in the constructor using the mocked dependencies — never inline
- Always implement `IDisposable` in test classes containing mocks
  - Call `VerifyNoOtherCalls()` on every mock in `Dispose` to catch unexpected interactions:

    ```csharp
        public void Dispose()
        {
            _flipClientMock.VerifyNoOtherCalls();
            _otherDependencyMock.VerifyNoOtherCalls();
        }
    ```
