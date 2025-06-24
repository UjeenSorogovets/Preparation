# Testing & Best Practices

[⬅️ Back to Table of Contents](README.md)

### 59. What is unit testing in .NET and why is it important?

**Answer:** Unit testing verifies individual units of code (methods, classes) in isolation. Benefits include regression prevention, design feedback, documentation, and enabling refactoring.

### 60. How do you mock dependencies in unit tests using Moq?

```csharp
var repoMock = new Mock<IUserRepository>();
repoMock.Setup(r => r.FindAsync(1)).ReturnsAsync(new User { Id = 1 });
var service = new UserService(repoMock.Object);
var user = await service.GetUserByIdAsync(1);
repoMock.VerifyAll();
```

### 61. Can you explain SOLID principles and how they relate to testing?

**Answer:** SOLID leads to loosely-coupled code with abstractions, making units easier to test and mock.

### 62. What is Continuous Integration/Continuous Deployment (CI/CD) for .NET projects?

- Use **GitHub Actions**, **Azure DevOps Pipelines**, or **GitLab CI**.
- Steps: restore ⇒ build ⇒ test ⇒ publish ⇒ deploy.
- Failing tests block the pipeline, ensuring quality.

### 63. How do you ensure your C# code is secure?

- Run **`dotnet list package --vulnerable`**.
- Static analyzers (SonarQube, Semgrep).
- Use **Data Protection API** for secrets.

### 64. What are some common performance issues in .NET applications and how do you address them?

- Excessive allocations (use PerfView, dotMemory)
- Blocking async calls (`.Result`)
- Chatty database queries (EF Core `Include`, batching)

### 65. Describe the Repository pattern and its benefits.

See Q44. Benefits: abstraction, unit testing, domain-centric.

### 66. How do you handle database migrations in Entity Framework?

`dotnet ef migrations add <Name>` then `dotnet ef database update`. Use **Idempotent scripts** for production.

### 67. What tools do you use for debugging and profiling .NET applications?

- Visual Studio Diagnostics Tools
- **dotnet-trace**, **dotnet-counters**
- PerfView, JetBrains dotTrace

### 68. How do you stay updated with the latest .NET technologies and practices?

Follow **.NET Blog**, GitHub repos, community stand-ups, conferences (Build, .NET Conf).

### 69. How do xUnit and Moq work together in unit tests?

```csharp
public class UserServiceTests
{
    [Fact]
    public async Task GetUser_ReturnsUser()
    {
        var repo = new Mock<IUserRepository>();
        repo.Setup(r => r.FindAsync(1)).ReturnsAsync(new User { Id = 1 });
        var service = new UserService(repo.Object);
        var result = await service.GetUserByIdAsync(1);
        Assert.Equal(1, result.Id);
    }
}
```

### 70. What is the purpose of WebApplicationFactory in integration tests?

`WebApplicationFactory<TEntryPoint>` (from `Microsoft.AspNetCore.Mvc.Testing`) spins up an in-memory TestServer so integration tests can send HTTP requests to your API without real hosting.

```csharp
var factory = new WebApplicationFactory<Program>();
var client = factory.CreateClient();
var response = await client.GetAsync("/api/users");
```

### 71. What does dotnet publish single-file/self-contained achieve?

- **Single-file** bundles assemblies + runtime into one executable.
- **Self-contained** includes the .NET runtime—no installation required.
- Good for microservices and side-by-side deployment. 