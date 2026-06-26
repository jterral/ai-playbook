---
paths:
  - "tests/**/*.cs"
---

# C# Conventions - Tests

## Libraries

- `xUnit` for unit tests
- `Moq` for mocking dependencies

## Test Class Structure

- Use `sealed` test classes to prevent inheritance and ensure isolation
- Declare mocks as `private readonly` fields, suffixed with `Mock` — e.g. `_myServiceMock`
- Declare the system under test as `private readonly _sut`
- Initialize mocks inline with `new Mock<T>()`
- Initialize `_sut` in the constructor using the mocked `.Object` properties — never inline
- Implement `IDisposable` and call `VerifyNoOtherCalls()` on every mock in `Dispose`

```csharp
public sealed class MyServiceTests : IDisposable
{
    private readonly Mock<IDependency> _dependencyMock = new();
    private readonly Mock<IOtherDependency> _otherDependencyMock = new();
    private readonly MyService _sut;

    public MyServiceTests()
    {
        _sut = new MyService(_dependencyMock.Object, _otherDependencyMock.Object);
    }

    public void Dispose()
    {
        _dependencyMock.VerifyNoOtherCalls();
        _otherDependencyMock.VerifyNoOtherCalls();
    }
}
```

## Test Methods

- Follow Arrange / Act / Assert — always add the three comments to separate sections
- Name tests as `MethodName_Scenario_ExpectedBehavior`
