# Architecture & Patterns

[⬅️ Back to Table of Contents](README.md)

### 43. Illustrate SOLID principles using dependency injection in .NET.

**Answer:** The **SOLID** principles guide maintainable OOP design. DI helps enforce them by decoupling classes.

1. **Single Responsibility (SRP):** Each class has one reason to change.
   ```csharp
   public interface IEmailSender { Task SendAsync(string to, string body); }
   public class SmtpEmailSender : IEmailSender { /* SMTP code */ }
   public class UserService
   {
       private readonly IEmailSender _email;
       public UserService(IEmailSender email) => _email = email; // DI
       public async Task RegisterAsync(User u)
       {
           /* validation + repo */
           await _email.SendAsync(u.Email, "Welcome!");
       }
   }
   ```
2. **Open/Closed (OCP):** Add new email provider by implementing `IEmailSender` without modifying `UserService`.
3. **Liskov (LSP):** Substitutable implementations (`SmtpEmailSender`, `SendGridEmailSender`).
4. **Interface Segregation (ISP):** Clients depend on minimal contracts (`IEmailSender`).
5. **Dependency Inversion (DIP):** High-level `UserService` depends on abstraction, not concrete SMTP class.

### 44. When and how would you use Repository + Unit of Work with EF Core?

**Answer:**
- **Repository** abstracts data access, exposing domain-centric operations.
- **Unit of Work** coordinates multiple repositories in a single transaction.

```csharp
public interface IUserRepository
{
    Task<User?> FindAsync(int id);
    void Add(User user);
}

public class UserRepository : IUserRepository
{
    private readonly DbContext _ctx;
    public UserRepository(DbContext ctx) => _ctx = ctx;
    public Task<User?> FindAsync(int id) => _ctx.Set<User>().FindAsync(id).AsTask();
    public void Add(User user) => _ctx.Set<User>().Add(user);
}

public interface IUnitOfWork : IAsyncDisposable
{
    IUserRepository Users { get; }
    Task<int> CommitAsync();
}

public class EfUnitOfWork : IUnitOfWork
{
    private readonly ApplicationDbContext _ctx;
    public EfUnitOfWork(ApplicationDbContext ctx) => _ctx = ctx;
    public IUserRepository Users => new UserRepository(_ctx);
    public Task<int> CommitAsync() => _ctx.SaveChangesAsync();
    public ValueTask DisposeAsync() => _ctx.DisposeAsync();
}
```

**Pros:**
- Testability (mock repositories)
- Transaction boundary in one place
- Persistence ignorance

**Cons:**
- Extra abstraction, may duplicate EF features (change tracking, LINQ)

### 45. Outline Clean Architecture layers in a C# solution.

```
┌───────────────────────┐
│        UI Layer       │  e.g., Web API, Blazor
└──────────▲────────────┘
           │ calls DTOs
┌──────────┴────────────┐
│  Application Layer    │  Use-cases, CQRS handlers
└──────────▲────────────┘
           │ interfaces
┌──────────┴────────────┐
│    Domain Layer       │  Entities, Value Objects, domain events
└──────────▲────────────┘
           │ abstraction
┌──────────┴────────────┐
│ Infrastructure Layer  │  EF Core, Email, File system
└────────────────────────┘
```

- **Dependency rule:** Flow of dependencies points **inwards**; outer layers depend on inner layers, never the opposite.
- **DTOs / Mappers:** Keep controllers independent from domain entities.
- **Benefits:** Testability, maintainability, separation of concerns. 