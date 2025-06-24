# Advanced

[⬅️ Back to Table of Contents](README.md)

### 21. What is reflection in .NET and when would you use it?

**Answer:** Reflection is the ability of a program to inspect and manipulate its own metadata at runtime. In .NET, the `System.Reflection` namespace allows you to:
- Discover assemblies, modules, types, and members at runtime
- Dynamically create instances of types
- Invoke methods and access fields or properties
- Emit Intermediate Language (IL) code dynamically (via `System.Reflection.Emit`)

**Use cases:**
- Plug-in architectures where types are loaded dynamically
- Serialization/deserialization frameworks (e.g., JSON serializers)
- ORMs mapping database columns to properties
- Unit-testing frameworks that discover tests via attributes
- Compilers and code generators

```csharp
// Loading an assembly and invoking a method via reflection
var assembly = Assembly.Load("MyPlugin");
var type = assembly.GetType("MyPlugin.PluginEntry");
var instance = Activator.CreateInstance(type);
var runMethod = type.GetMethod("Run");
runMethod.Invoke(instance, null);
```

### 22. Explain how middleware works internally in ASP.NET Core.

**Answer:** Each middleware component is a delegate of type `RequestDelegate` with the signature `Task(RequestDelegate next)` or `Task(HttpContext context, RequestDelegate next)`.

- Middleware are registered in `Startup.Configure` via extension methods like `UseRouting()`.
- ASP.NET Core builds a linked list where each middleware holds a reference to the *next* delegate.
- The hosting layer passes the `HttpContext` to the first middleware. Each component can:
  1. Execute code *before* calling `await next(context);`
  2. Optionally short-circuit the pipeline (e.g., authentication failure)
  3. Execute code *after* the next component returns (post-processing)

```csharp
public class SampleMiddleware
{
    private readonly RequestDelegate _next;

    public SampleMiddleware(RequestDelegate next) => _next = next;

    public async Task InvokeAsync(HttpContext context)
    {
        // pre-processing
        await _next(context);
        // post-processing
    }
}
```

### 23. Describe dependency injection (DI) lifetimes in ASP.NET Core.

**Answer:**
- **Singleton:** One instance for the entire application lifetime (`AddSingleton`).
- **Scoped:** One instance per client request (`AddScoped`).
- **Transient:** New instance every time it's requested (`AddTransient`).

Choosing the wrong lifetime can cause **captive-dependency** problems (a singleton depending on a scoped service) or memory leaks.

### 24. What is the purpose of .NET Standard and is it still relevant today?

**Answer:** .NET Standard was a formal specification of BCL APIs that all .NET implementations had to implement (.NET Framework, .NET Core, Xamarin, etc.). It solved "code sharing" problem between multiple, divergent platforms.

Since .NET 5 the ecosystem converged into a **single unified platform** (current LTS is .NET 8). Therefore, new code should target `net6.0` / `net8.0` **TFMs** instead of `netstandard`. .NET Standard remains relevant only for libraries that must run on legacy .NET Framework 4.x.

### 25. Compare .NET Framework 4.8, .NET 8, and Mono/Xamarin.

| Feature | .NET Framework 4.8 | .NET 8 (Current) | Mono / Xamarin |
|---------|-------------------|------------------|----------------|
| Release year | 2019 (last) | 2023 | 2009+ |
| Platforms | Windows only | Windows / Linux / macOS | Mobile (iOS/Android), WASM |
| Open Source | No | Yes | Yes |
| GC / JIT | Legacy GC, RyuJIT (x64 only) | Server+Workstation GC, SGen, Dynamic PGO | SGen GC, Ahead-of-Time (iOS) |
| Future | Security fixes only | Active development | Replaced by .NET MAUI |

### 26. How does the garbage collector work internally and how can you optimize it?

**Answer:** .NET uses a generational, mark-and-compact GC with three generations (0,1,2) plus the Large Object Heap (LOH). Optimizations:
- Avoid allocating on hot paths (measure with PerfView / dotnet-trace)
- Pool objects (ArrayPool/MemoryPool)
- Use `Span<T>` / `stackalloc` to avoid heap allocations
- Enable *server* GC for throughput or *background* GC for latency
- For high-throughput apps, pin fewer objects to reduce fragmentation

### 27. What are attributes in C# and how does the runtime use them?

**Answer:** Attributes are metadata added to assemblies, types, members or parameters. At runtime they are accessed via reflection (`GetCustomAttributes`). The CLR uses attributes for:
- Serialization (`[Serializable]`, `[JsonProperty]`)
- P/Invoke (`[DllImport]`)
- Security (`[Authorize]`)
- Unit tests (`[Fact]`, `[TestMethod]`)

Custom attributes must inherit from `System.Attribute` and can have positional or named arguments.

### 28. Describe the compilation pipeline from C# source code to native code.

1. **Roslyn (csc)** compiles C# into **IL** + metadata inside a PE file (.dll/.exe).
2. At startup, the **CLR loader** verifies metadata, resolves references, and JITs methods on-demand using **RyuJIT** (or AOT with NativeAOT).
3. The JIT performs tiered compilation: quick Tier 0 for startup, optimized Tier 1 with PGO.
4. The OS loader maps native code pages; execution proceeds.

### 29. What is the Global Assembly Cache (GAC) and why was it introduced?

**Answer:** The GAC is a machine-wide store for strong-named assemblies (signed with a public/private key). It solved "DLL Hell" by allowing multiple versions of the same assembly to coexist. In modern .NET (Core/5+) the GAC is not used; assemblies are resolved from the application base directory or NuGet cache, enhancing side-by-side deployment.

### 30. How would you secure an ASP.NET Core web application?

Key practices:
- Use **HTTPS** and HSTS (`UseHttpsRedirection`, `UseHsts`)
- Implement **Content Security Policy** and other security headers
- Apply **OWASP Top 10** mitigations (XSS, CSRF, etc.)
- Store secrets in **Azure Key Vault** / **AWS Secrets Manager**
- Use **ASP.NET Core Identity** or external IdP (OpenID Connect)
- Validate input and use **model binding validation**
- Enable **SameSite** cookies and secure flags
- Keep packages up-to-date and run `dotnet list package --vulnerable` 