# Framework-Specific

[⬅️ Back to Table of Contents](README.md)

### 46. What is the MVC pattern and how is it implemented in ASP.NET Core?

**Answer:** MVC separates an application into **Model**, **View**, and **Controller**. In ASP.NET Core:
- **Model**: POCO classes + validation attributes + EF Core entities.
- **View**: Razor templates (`.cshtml`) rendered server-side.
- **Controller**: C# classes inheriting `Controller` that handle HTTP requests, orchestrate models, and return views or data.

Benefits: testability, separation of concerns, multiple view engines.

### 47. Razor Pages vs MVC Controllers—when to choose each?

**Answer:**
- **Razor Pages** consolidates request handling and page rendering into a single `.cshtml` file + `@functions`/code-behind class. Ideal for page-centric CRUD sites.
- **MVC Controllers** provide fine-grained routing, API responses, multiple views per controller. Better for complex apps or Web APIs.

### 48. How do you perform validations in ASP.NET Core?

- **Data Annotations** (`[Required]`, `[Range]`) on model properties.
- **FluentValidation** library for complex rules.
- **ModelState** checked in controllers (`if(!ModelState.IsValid) ...`).
- **Client-side validation** via unobtrusive JavaScript.

### 49. Describe SignalR and its use cases.

**Answer:** SignalR is a real-time communication library that abstracts WebSockets, Server-Sent Events and Long Polling. Use cases: chat, notifications, dashboards, multiplayer games.

```csharp
services.AddSignalR();
app.MapHub<ChatHub>("/chat");
```

### 50. What are the benefits of using Minimal APIs in .NET 7/8 compared to traditional controllers?

- Less boilerplate; single file endpoints (`app.MapGet(...)`).
- Faster cold-start (fewer DI services).
- Ideal for microservices and serverless.
- Still supports filters, DI, OpenAPI via `SwaggerGen`.

### 51. How do you implement API versioning in ASP.NET Core?

Add NuGet `Microsoft.AspNetCore.Mvc.Versioning` then:
```csharp
services.AddApiVersioning(o =>
{
    o.DefaultApiVersion = new ApiVersion(1,0);
    o.AssumeDefaultVersionWhenUnspecified = true;
    o.ReportApiVersions = true;
});
```
Version via URL (`/v2/products`), header (`api-version`), or media type.

### 52. What is IApplicationBuilder and what happens during application startup?

`IApplicationBuilder` builds the middleware pipeline inside `Program.cs/Startup.Configure`. Each `UseXyz` extension adds middleware delegates to a list executed per request.

### 53. Explain Areas in MVC and their purpose.

Areas partition a large MVC app into smaller functional sections with their own `Controllers`, `Views` and `Models` folders (e.g., `/Areas/Admin/...`). Routing template: `area`, `controller`, `action`.

### 54. How do you manage sessions in ASP.NET Core applications?

Add `services.AddSession()` and `app.UseSession()`. Data stored in memory or distributed cache (Redis, SQL). Access via `HttpContext.Session.SetString()`.

### 55. Describe how to implement caching in ASP.NET Core.

- **Response caching** (`[ResponseCache]`, `UseResponseCaching`).
- **In-memory cache** (`IMemoryCache`).
- **Distributed cache** (`IDistributedCache`, Redis).
- **Output caching** (ASP.NET Core 8) for full response reuse.

### 56. Why is middleware order critical?

Because the pipeline is **ordered**. For example, `UseRouting` must come before `UseAuthorization`. Incorrect order can break auth, CORS, exception handling.

### 57. How do you secure an API with JWT in ASP.NET Core?

Add `AddAuthentication().AddJwtBearer(...)`; issue tokens via IdentityServer/Azure AD; protect endpoints with `[Authorize]`. Validate issuer, audience, expiration, signing key.

### 58. What are the major changes introduced in .NET 8 for web applications?

- **Native AOT publishing** for ASP.NET Core minimal APIs.
- **Output caching middleware**.
- Improvements to **rate limiting** and **authentication handlers**.
- **Blazor United** (server + webassembly hybrid).
- HTTP/3 enabled by default. 