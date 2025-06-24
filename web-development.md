# Web Development

[⬅️ К оглавлению](README.md)

### 61. What is ASP.NET Core and how does it differ from ASP.NET Framework?

**Answer:** ASP.NET Core is a cross-platform, high-performance framework for building modern, cloud-based, internet-connected applications. It's a complete rewrite of ASP.NET Framework with several key differences:

**Key Differences:**

**Cross-Platform Support:**
- ASP.NET Core runs on Windows, macOS, and Linux
- ASP.NET Framework is Windows-only

**Performance:**
- ASP.NET Core is significantly faster
- Built on .NET Core (now .NET 5+) which is more performant
- Optimized for cloud and microservices

**Dependency Injection:**
- Built-in DI container in ASP.NET Core
- ASP.NET Framework requires third-party DI containers

**Configuration:**
- JSON-based configuration in ASP.NET Core
- Web.config in ASP.NET Framework

**Middleware Pipeline:**
- Modular middleware pipeline in ASP.NET Core
- HTTP modules and handlers in ASP.NET Framework

```csharp
// ASP.NET Core Startup
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddControllers();
        services.AddDbContext<ApplicationDbContext>();
    }

    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        if (env.IsDevelopment())
        {
            app.UseDeveloperExceptionPage();
        }

        app.UseRouting();
        app.UseEndpoints(endpoints =>
        {
            endpoints.MapControllers();
        });
    }
}

// ASP.NET Core Controller
[ApiController]
[Route("api/[controller]")]
public class UsersController : ControllerBase
{
    private readonly IUserService _userService;

    public UsersController(IUserService userService)
    {
        _userService = userService;
    }

    [HttpGet]
    public async Task<ActionResult<IEnumerable<User>>> GetUsers()
    {
        var users = await _userService.GetUsersAsync();
        return Ok(users);
    }
}
```

### 62. Explain the middleware pipeline in ASP.NET Core.

**Answer:** Middleware in ASP.NET Core is software that's assembled into an application pipeline to handle requests and responses. Each middleware component chooses whether to pass the request to the next component in the pipeline, and can perform certain actions before and after the next component.

**Middleware Pipeline:**
```csharp
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    // Exception handling middleware
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }
    else
    {
        app.UseExceptionHandler("/Error");
        app.UseHsts();
    }

    // HTTPS redirection
    app.UseHttpsRedirection();

    // Static files
    app.UseStaticFiles();

    // Routing
    app.UseRouting();

    // Authentication
    app.UseAuthentication();

    // Authorization
    app.UseAuthorization();

    // Endpoints
    app.UseEndpoints(endpoints =>
    {
        endpoints.MapControllers();
        endpoints.MapRazorPages();
    });
}
```

**Custom Middleware:**
```csharp
// Custom middleware class
public class RequestLoggingMiddleware
{
    private readonly RequestDelegate _next;
    private readonly ILogger _logger;

    public RequestLoggingMiddleware(RequestDelegate next, ILogger<RequestLoggingMiddleware> logger)
    {
        _next = next;
        _logger = logger;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        _logger.LogInformation($"Request: {context.Request.Method} {context.Request.Path}");

        await _next(context);

        _logger.LogInformation($"Response: {context.Response.StatusCode}");
    }
}

// Extension method for easy registration
public static class RequestLoggingMiddlewareExtensions
{
    public static IApplicationBuilder UseRequestLogging(this IApplicationBuilder builder)
    {
        return builder.UseMiddleware<RequestLoggingMiddleware>();
    }
}

// Usage in Configure method
app.UseRequestLogging();
```

**Inline Middleware:**
```csharp
app.Use(async (context, next) =>
{
    var start = DateTime.UtcNow;
    
    await next();
    
    var elapsed = DateTime.UtcNow - start;
    context.Response.Headers.Add("X-Response-Time", elapsed.TotalMilliseconds.ToString());
});
```

### 63. What is dependency injection and how is it implemented in ASP.NET Core?

**Answer:** Dependency Injection (DI) is a design pattern that implements Inversion of Control (IoC) for managing dependencies. ASP.NET Core has a built-in DI container that manages the creation and lifetime of objects.

**Service Registration:**
```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Singleton - one instance for the entire application
    services.AddSingleton<IConfigurationService, ConfigurationService>();
    
    // Scoped - one instance per request
    services.AddScoped<IUserService, UserService>();
    
    // Transient - new instance every time
    services.AddTransient<IEmailService, EmailService>();
    
    // Register with interface
    services.AddScoped<IUserRepository, UserRepository>();
    
    // Register with factory
    services.AddScoped<IUserService>(provider =>
    {
        var repository = provider.GetService<IUserRepository>();
        var logger = provider.GetService<ILogger<UserService>>();
        return new UserService(repository, logger);
    });
}
```

**Constructor Injection:**
```csharp
public class UsersController : ControllerBase
{
    private readonly IUserService _userService;
    private readonly ILogger<UsersController> _logger;

    public UsersController(IUserService userService, ILogger<UsersController> logger)
    {
        _userService = userService;
        _logger = logger;
    }

    [HttpGet]
    public async Task<ActionResult<IEnumerable<User>>> GetUsers()
    {
        _logger.LogInformation("Getting users");
        var users = await _userService.GetUsersAsync();
        return Ok(users);
    }
}
```

**Service Implementation:**
```csharp
public interface IUserService
{
    Task<IEnumerable<User>> GetUsersAsync();
    Task<User> GetUserByIdAsync(int id);
}

public class UserService : IUserService
{
    private readonly IUserRepository _repository;
    private readonly ILogger<UserService> _logger;

    public UserService(IUserRepository repository, ILogger<UserService> logger)
    {
        _repository = repository;
        _logger = logger;
    }

    public async Task<IEnumerable<User>> GetUsersAsync()
    {
        _logger.LogInformation("Retrieving all users");
        return await _repository.GetAllAsync();
    }

    public async Task<User> GetUserByIdAsync(int id)
    {
        _logger.LogInformation($"Retrieving user with ID: {id}");
        return await _repository.GetByIdAsync(id);
    }
}
```

### 64. What is the difference between ViewData, ViewBag, and TempData in ASP.NET Core?

**Answer:** These are different ways to pass data from controllers to views in ASP.NET Core MVC:

**ViewData:**
- Dictionary object that inherits from ViewDataDictionary
- Requires type casting
- Available only for the current request
- Strongly typed when used with ViewDataDictionary<T>

**ViewBag:**
- Dynamic property that uses ViewData internally
- No type casting required
- Available only for the current request
- Less performant than ViewData

**TempData:**
- Dictionary object that persists data between requests
- Uses session storage
- Automatically deleted after being read
- Useful for redirect scenarios

```csharp
// Controller
public class HomeController : Controller
{
    public IActionResult Index()
    {
        // ViewData
        ViewData["Message"] = "Hello from ViewData";
        ViewData["Users"] = new List<string> { "John", "Jane" };

        // ViewBag
        ViewBag.Message = "Hello from ViewBag";
        ViewBag.Users = new List<string> { "John", "Jane" };

        // TempData
        TempData["SuccessMessage"] = "Operation completed successfully";

        return View();
    }

    public IActionResult Create()
    {
        // Process form data
        // ...

        TempData["SuccessMessage"] = "User created successfully";
        return RedirectToAction("Index");
    }
}
```

**View Usage:**
```html
@{
    ViewData["Title"] = "Home Page";
}

<!-- ViewData -->
<h1>@ViewData["Message"]</h1>
<ul>
    @foreach (var user in (List<string>)ViewData["Users"])
    {
        <li>@user</li>
    }
</ul>

<!-- ViewBag -->
<h1>@ViewBag.Message</h1>
<ul>
    @foreach (var user in ViewBag.Users)
    {
        <li>@user</li>
    }
</ul>

<!-- TempData -->
@if (TempData["SuccessMessage"] != null)
{
    <div class="alert alert-success">
        @TempData["SuccessMessage"]
    </div>
}
```

### 65. Explain authentication and authorization in ASP.NET Core.

**Answer:** Authentication verifies who a user is, while authorization determines what a user can access.

**Authentication:**
```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Add authentication
    services.AddAuthentication(options =>
    {
        options.DefaultAuthenticateScheme = CookieAuthenticationDefaults.AuthenticationScheme;
        options.DefaultSignInScheme = CookieAuthenticationDefaults.AuthenticationScheme;
        options.DefaultChallengeScheme = CookieAuthenticationDefaults.AuthenticationScheme;
    })
    .AddCookie(options =>
    {
        options.LoginPath = "/Account/Login";
        options.LogoutPath = "/Account/Logout";
        options.AccessDeniedPath = "/Account/AccessDenied";
    })
    .AddJwtBearer(options =>
    {
        options.TokenValidationParameters = new TokenValidationParameters
        {
            ValidateIssuer = true,
            ValidateAudience = true,
            ValidateLifetime = true,
            ValidateIssuerSigningKey = true,
            ValidIssuer = Configuration["Jwt:Issuer"],
            ValidAudience = Configuration["Jwt:Audience"],
            IssuerSigningKey = new SymmetricSecurityKey(
                Encoding.UTF8.GetBytes(Configuration["Jwt:Key"]))
        };
    });
}

public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    // Use authentication
    app.UseAuthentication();
    app.UseAuthorization();
}
```

**Login Controller:**
```csharp
[HttpPost]
public async Task<IActionResult> Login(LoginViewModel model)
{
    if (ModelState.IsValid)
    {
        var user = await _userService.ValidateUserAsync(model.Username, model.Password);
        
        if (user != null)
        {
            var claims = new List<Claim>
            {
                new Claim(ClaimTypes.Name, user.Username),
                new Claim(ClaimTypes.NameIdentifier, user.Id.ToString()),
                new Claim(ClaimTypes.Role, user.Role)
            };

            var claimsIdentity = new ClaimsIdentity(claims, CookieAuthenticationDefaults.AuthenticationScheme);
            var authProperties = new AuthenticationProperties
            {
                IsPersistent = model.RememberMe
            };

            await HttpContext.SignInAsync(
                CookieAuthenticationDefaults.AuthenticationScheme,
                new ClaimsPrincipal(claimsIdentity),
                authProperties);

            return RedirectToAction("Index", "Home");
        }
    }

    ModelState.AddModelError("", "Invalid login attempt");
    return View(model);
}
```

**Authorization:**
```csharp
// Controller-level authorization
[Authorize]
public class AdminController : Controller
{
    [Authorize(Roles = "Admin")]
    public IActionResult Index()
    {
        return View();
    }

    [Authorize(Policy = "MinimumAge")]
    public IActionResult AgeRestricted()
    {
        return View();
    }
}

// Action-level authorization
[AllowAnonymous]
public IActionResult PublicAction()
{
    return View();
}

[Authorize(Roles = "Admin,Manager")]
public IActionResult ManagerAction()
{
    return View();
}
```

**Custom Authorization Policy:**
```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddAuthorization(options =>
    {
        options.AddPolicy("MinimumAge", policy =>
            policy.RequireAssertion(context =>
                context.User.HasClaim(c => 
                    c.Type == "Age" && 
                    int.TryParse(c.Value, out int age) && 
                    age >= 18)));
    });
}
```

### 66. What is Entity Framework Core and how does it work?

**Answer:** Entity Framework Core is a modern, lightweight, extensible, and cross-platform version of Entity Framework. It's an object-relational mapping (ORM) framework that enables .NET developers to work with a database using .NET objects.

**DbContext:**
```csharp
public class ApplicationDbContext : DbContext
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }

    public DbSet<User> Users { get; set; }
    public DbSet<Order> Orders { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        // Configure entity relationships
        modelBuilder.Entity<User>()
            .HasMany(u => u.Orders)
            .WithOne(o => o.User)
            .HasForeignKey(o => o.UserId);

        // Configure entity properties
        modelBuilder.Entity<User>()
            .Property(u => u.Email)
            .IsRequired()
            .HasMaxLength(100);

        modelBuilder.Entity<User>()
            .HasIndex(u => u.Email)
            .IsUnique();
    }
}
```

**Entity Models:**
```csharp
public class User
{
    public int Id { get; set; }
    public string Username { get; set; }
    public string Email { get; set; }
    public DateTime CreatedAt { get; set; }
    
    // Navigation property
    public virtual ICollection<Order> Orders { get; set; }
}

public class Order
{
    public int Id { get; set; }
    public int UserId { get; set; }
    public decimal TotalAmount { get; set; }
    public DateTime OrderDate { get; set; }
    
    // Navigation property
    public virtual User User { get; set; }
}
```

**CRUD Operations:**
```csharp
public class UserService
{
    private readonly ApplicationDbContext _context;

    public UserService(ApplicationDbContext context)
    {
        _context = context;
    }

    // Create
    public async Task<User> CreateUserAsync(User user)
    {
        _context.Users.Add(user);
        await _context.SaveChangesAsync();
        return user;
    }

    // Read
    public async Task<User> GetUserByIdAsync(int id)
    {
        return await _context.Users
            .Include(u => u.Orders)
            .FirstOrDefaultAsync(u => u.Id == id);
    }

    public async Task<IEnumerable<User>> GetUsersAsync()
    {
        return await _context.Users
            .Include(u => u.Orders)
            .ToListAsync();
    }

    // Update
    public async Task UpdateUserAsync(User user)
    {
        _context.Users.Update(user);
        await _context.SaveChangesAsync();
    }

    // Delete
    public async Task DeleteUserAsync(int id)
    {
        var user = await _context.Users.FindAsync(id);
        if (user != null)
        {
            _context.Users.Remove(user);
            await _context.SaveChangesAsync();
        }
    }
}
```

**LINQ Queries:**
```csharp
// Simple query
var users = await _context.Users
    .Where(u => u.CreatedAt >= DateTime.Today.AddDays(-30))
    .ToListAsync();

// Complex query with joins
var userOrders = await _context.Users
    .SelectMany(u => u.Orders, (user, order) => new
    {
        UserName = user.Username,
        OrderId = order.Id,
        OrderAmount = order.TotalAmount
    })
    .Where(uo => uo.OrderAmount > 100)
    .OrderByDescending(uo => uo.OrderAmount)
    .ToListAsync();

// Raw SQL
var users = await _context.Users
    .FromSqlRaw("SELECT * FROM Users WHERE CreatedAt >= {0}", DateTime.Today.AddDays(-30))
    .ToListAsync();
```

### 67. What are the different ways to handle errors in ASP.NET Core?

**Answer:** ASP.NET Core provides multiple ways to handle errors at different levels:

**Exception Handling Middleware:**
```csharp
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }
    else
    {
        app.UseExceptionHandler("/Error");
        app.UseHsts();
    }
}
```

**Custom Exception Handler:**
```csharp
public class CustomExceptionHandlerMiddleware
{
    private readonly RequestDelegate _next;
    private readonly ILogger<CustomExceptionHandlerMiddleware> _logger;

    public CustomExceptionHandlerMiddleware(RequestDelegate next, ILogger<CustomExceptionHandlerMiddleware> logger)
    {
        _next = next;
        _logger = logger;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        try
        {
            await _next(context);
        }
        catch (Exception ex)
        {
            _logger.LogError(ex, "An unhandled exception occurred");
            await HandleExceptionAsync(context, ex);
        }
    }

    private static async Task HandleExceptionAsync(HttpContext context, Exception exception)
    {
        context.Response.ContentType = "application/json";
        
        var response = new
        {
            error = new
            {
                message = "An error occurred processing your request.",
                details = exception.Message
            }
        };

        context.Response.StatusCode = exception switch
        {
            ArgumentException => 400,
            UnauthorizedAccessException => 401,
            NotFoundException => 404,
            _ => 500
        };

        await context.Response.WriteAsJsonAsync(response);
    }
}
```

**Controller-Level Exception Handling:**
```csharp
[ApiController]
public class UsersController : ControllerBase
{
    [HttpGet("{id}")]
    public async Task<ActionResult<User>> GetUser(int id)
    {
        try
        {
            var user = await _userService.GetUserByIdAsync(id);
            if (user == null)
            {
                return NotFound($"User with ID {id} not found");
            }
            return Ok(user);
        }
        catch (ArgumentException ex)
        {
            return BadRequest(ex.Message);
        }
        catch (Exception ex)
        {
            _logger.LogError(ex, "Error retrieving user {UserId}", id);
            return StatusCode(500, "An error occurred while processing your request");
        }
    }
}
```

**Global Exception Filter:**
```csharp
public class GlobalExceptionFilter : IExceptionFilter
{
    private readonly ILogger<GlobalExceptionFilter> _logger;

    public GlobalExceptionFilter(ILogger<GlobalExceptionFilter> logger)
    {
        _logger = logger;
    }

    public void OnException(ExceptionContext context)
    {
        _logger.LogError(context.Exception, "An unhandled exception occurred");

        var result = new ObjectResult(new
        {
            error = new
            {
                message = "An error occurred processing your request.",
                details = context.Exception.Message
            }
        })
        {
            StatusCode = 500
        };

        context.Result = result;
        context.ExceptionHandled = true;
    }
}

// Register in ConfigureServices
services.AddControllers(options =>
{
    options.Filters.Add<GlobalExceptionFilter>();
});
```

**Custom Exceptions:**
```csharp
public class NotFoundException : Exception
{
    public NotFoundException(string message) : base(message) { }
}

public class ValidationException : Exception
{
    public ValidationException(string message) : base(message) { }
}

// Usage
public async Task<User> GetUserByIdAsync(int id)
{
    var user = await _context.Users.FindAsync(id);
    if (user == null)
    {
        throw new NotFoundException($"User with ID {id} not found");
    }
    return user;
}
```

### 68. What is the difference between synchronous and asynchronous programming in ASP.NET Core?

**Answer:** Synchronous programming blocks the thread while waiting for operations to complete, while asynchronous programming allows the thread to be freed up to handle other requests while waiting.

**Synchronous Example:**
```csharp
public class SyncController : Controller
{
    public IActionResult GetData()
    {
        // This blocks the thread
        var data = _service.GetData();
        return Ok(data);
    }

    public IActionResult GetUser(int id)
    {
        // This also blocks the thread
        var user = _userService.GetUserById(id);
        return Ok(user);
    }
}
```

**Asynchronous Example:**
```csharp
public class AsyncController : Controller
{
    public async Task<IActionResult> GetDataAsync()
    {
        // This doesn't block the thread
        var data = await _service.GetDataAsync();
        return Ok(data);
    }

    public async Task<IActionResult> GetUserAsync(int id)
    {
        // This doesn't block the thread
        var user = await _userService.GetUserByIdAsync(id);
        return Ok(user);
    }

    public async Task<IActionResult> GetMultipleUsersAsync()
    {
        // Parallel execution
        var task1 = _userService.GetUserByIdAsync(1);
        var task2 = _userService.GetUserByIdAsync(2);
        var task3 = _userService.GetUserByIdAsync(3);

        await Task.WhenAll(task1, task2, task3);

        var result = new
        {
            User1 = await task1,
            User2 = await task2,
            User3 = await task3
        };

        return Ok(result);
    }
}
```

**Benefits of Async Programming:**
- Better scalability (more concurrent requests)
- Better resource utilization
- Improved responsiveness
- Better user experience

**When to Use Async:**
- I/O operations (database, file system, network)
- Long-running operations
- Operations that can be parallelized
- Web API endpoints

### 69. Explain the concept of middleware in ASP.NET Core with examples.

**Answer:** Middleware is software that's assembled into an application pipeline to handle requests and responses. Each middleware component can perform operations before and after the next component in the pipeline.

**Built-in Middleware:**
```csharp
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    // Exception handling
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }
    else
    {
        app.UseExceptionHandler("/Error");
        app.UseHsts();
    }

    // HTTPS redirection
    app.UseHttpsRedirection();

    // Static files
    app.UseStaticFiles();

    // Routing
    app.UseRouting();

    // CORS
    app.UseCors("AllowAll");

    // Authentication
    app.UseAuthentication();

    // Authorization
    app.UseAuthorization();

    // Endpoints
    app.UseEndpoints(endpoints =>
    {
        endpoints.MapControllers();
        endpoints.MapRazorPages();
    });
}
```

**Custom Middleware:**
```csharp
public class RequestLoggingMiddleware
{
    private readonly RequestDelegate _next;
    private readonly ILogger _logger;

    public RequestLoggingMiddleware(RequestDelegate next, ILogger<RequestLoggingMiddleware> logger)
    {
        _next = next;
        _logger = logger;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        var start = DateTime.UtcNow;
        var requestPath = context.Request.Path;

        _logger.LogInformation($"Request started: {context.Request.Method} {requestPath}");

        try
        {
            await _next(context);
        }
        finally
        {
            var elapsed = DateTime.UtcNow - start;
            _logger.LogInformation($"Request completed: {context.Request.Method} {requestPath} - {context.Response.StatusCode} in {elapsed.TotalMilliseconds}ms");
        }
    }
}

// Extension method
public static class RequestLoggingMiddlewareExtensions
{
    public static IApplicationBuilder UseRequestLogging(this IApplicationBuilder builder)
    {
        return builder.UseMiddleware<RequestLoggingMiddleware>();
    }
}

// Usage
app.UseRequestLogging();
```

**Inline Middleware:**
```csharp
app.Use(async (context, next) =>
{
    var start = DateTime.UtcNow;
    
    // Do something before the next middleware
    context.Response.Headers.Add("X-Request-Start", start.ToString("O"));
    
    await next();
    
    // Do something after the next middleware
    var elapsed = DateTime.UtcNow - start;
    context.Response.Headers.Add("X-Request-Duration", elapsed.TotalMilliseconds.ToString());
});
```

**Conditional Middleware:**
```csharp
app.UseWhen(context => context.Request.Path.StartsWithSegments("/api"), appBuilder =>
{
    appBuilder.Use(async (context, next) =>
    {
        // Add API-specific headers
        context.Response.Headers.Add("X-API-Version", "1.0");
        await next();
    });
});
```

### 70. What is the difference between IActionResult and ActionResult in ASP.NET Core?

**Answer:** Both are used to return results from controller actions, but they have different purposes:

**IActionResult:**
- Interface that represents different types of action results
- More flexible and extensible
- Used when you want to return different types of results conditionally

**ActionResult:**
- Abstract base class that implements IActionResult
- More specific and type-safe
- Used when you know the exact type you want to return

**Examples:**
```csharp
public class UsersController : ControllerBase
{
    // Using IActionResult - flexible return types
    public IActionResult GetUser(int id)
    {
        var user = _userService.GetUserById(id);
        
        if (user == null)
        {
            return NotFound(); // Returns NotFoundResult
        }
        
        return Ok(user); // Returns OkObjectResult
    }

    // Using ActionResult<T> - type-safe
    public ActionResult<User> GetUserTyped(int id)
    {
        var user = _userService.GetUserById(id);
        
        if (user == null)
        {
            return NotFound(); // Still returns NotFoundResult
        }
        
        return user; // Automatically wrapped in OkObjectResult
    }

    // Using specific return types
    public OkObjectResult GetUserOk(int id)
    {
        var user = _userService.GetUserById(id);
        return Ok(user);
    }

    public User GetUserDirect(int id)
    {
        return _userService.GetUserById(id);
    }
}
```

**Common Action Results:**
```csharp
// Success responses
return Ok(data);                    // 200 OK
return Created(uri, data);          // 201 Created
return Accepted();                  // 202 Accepted
return NoContent();                 // 204 No Content

// Client error responses
return BadRequest();                // 400 Bad Request
return Unauthorized();              // 401 Unauthorized
return Forbid();                    // 403 Forbidden
return NotFound();                  // 404 Not Found
return Conflict();                  // 409 Conflict

// Server error responses
return StatusCode(500);             // 500 Internal Server Error
return StatusCode(503);             // 503 Service Unavailable

// Redirect responses
return Redirect(url);               // 302 Found
return RedirectPermanent(url);      // 301 Moved Permanently
return LocalRedirect(url);          // 302 Found (local URL only)

// File responses
return File(bytes, contentType);    // File download
return PhysicalFile(path, type);    // Physical file
return VirtualFile(path, type);     // Virtual file

// View responses
return View();                      // View result
return View(model);                 // View with model
return PartialView();               // Partial view
```