# Performance and Memory

[⬅️ Back to Table of Contents](README.md)

### 37. How do GC generations and the Large Object Heap work?

**Answer:** Objects start in Gen 0; if still referenced after a collection they're promoted to Gen 1, then Gen 2. Objects ≥ 85 KB go straight to the LOH which is collected only with Gen 2 and, since .NET 6, can be compacted on demand (GCSettings.LargeObjectHeapCompactionMode).

**GC Generations:**
```csharp
// Objects start in Gen 0
var shortLived = new List<int>(); // Gen 0

// If still alive after Gen 0 collection, promoted to Gen 1
GC.Collect(0); // Collect only Gen 0
// shortLived might be promoted to Gen 1 if still referenced

// If still alive after Gen 1 collection, promoted to Gen 2
GC.Collect(1); // Collect Gen 0 and Gen 1
// shortLived might be promoted to Gen 2 if still referenced

// Large objects (≥ 85 KB) go directly to LOH
var largeArray = new byte[100000]; // Goes to LOH immediately
```

**Large Object Heap (LOH):**
```csharp
// LOH compaction (available since .NET 6)
GCSettings.LargeObjectHeapCompactionMode = GCLargeObjectHeapCompactionMode.CompactOnce;
GC.Collect(); // This will compact the LOH
```

**Why generations matter:**
- Gen 0 collections are fast and frequent
- Gen 2 collections are slow and rare
- Most objects die young (Gen 0)
- Long-lived objects eventually reach Gen 2

**.NET 9 update:** Dynamic PGO (profile-guided optimization) is enabled by default and updated live without restarts, further reducing Gen 2 collections by optimizing hot paths.

### 38. Name typical managed-memory leaks in long-running services.

**Answer:** Unsubscribed event handlers, static caches that outlive requests, misuse of HttpClient singletons with mutable default headers, and neglected IDisposable fields keep references alive and block GC, leading to steadily growing Gen 2/LOH usage.

**Event Handler Leaks:**
```csharp
public class EventLeakExample
{
    private static event EventHandler<string> GlobalEvent;
    
    public void Subscribe()
    {
        // LEAK: This subscription never gets unsubscribed
        GlobalEvent += OnEvent;
    }
    
    private void OnEvent(object sender, string data) { }
    
    // FIX: Unsubscribe when done
    public void Unsubscribe()
    {
        GlobalEvent -= OnEvent;
    }
}
```

**Static Cache Leaks:**
```csharp
public class CacheLeakExample
{
    // LEAK: Static cache grows indefinitely
    private static readonly Dictionary<string, object> _cache = new();
    
    public void AddToCache(string key, object value)
    {
        _cache[key] = value; // Never removed
    }
    
    // FIX: Use weak references or implement cleanup
    private static readonly ConditionalWeakTable<string, object> _weakCache = new();
}
```

**HttpClient Misuse:**
```csharp
// LEAK: Creating new HttpClient instances
public class BadHttpClientUsage
{
    public async Task<string> GetDataAsync()
    {
        using var client = new HttpClient(); // Creates new instance each time
        return await client.GetStringAsync("https://api.example.com");
    }
}

// FIX: Use HttpClientFactory or static instance
public class GoodHttpClientUsage
{
    private static readonly HttpClient _client = new();
    
    public async Task<string> GetDataAsync()
    {
        return await _client.GetStringAsync("https://api.example.com");
    }
}
```

### 39. Why is boxing/unboxing often highlighted in performance reviews?

**Answer:** Boxing allocates a fresh object to store a value-type and copies its data; unboxing only copies the value back. In tight loops this hidden allocation plus virtual dispatch can dominate CPU samples—generic numeric code avoids it entirely.

**Boxing Example:**
```csharp
// Boxing occurs when value types are treated as objects
int number = 42;
object boxed = number; // Boxing: allocates object on heap

// Unboxing when converting back
int unboxed = (int)boxed; // Unboxing: copies value back to stack

// Performance impact in loops
public void BoxingInLoop()
{
    var list = new ArrayList(); // Non-generic, causes boxing
    
    for (int i = 0; i < 1000000; i++)
    {
        list.Add(i); // Boxing occurs for each int
    }
}

// Better approach - no boxing
public void NoBoxingInLoop()
{
    var list = new List<int>(); // Generic, no boxing
    
    for (int i = 0; i < 1000000; i++)
    {
        list.Add(i); // No boxing
    }
}
```

**Generic Constraints Avoid Boxing:**
```csharp
// Without constraint - potential boxing
public class Container<T>
{
    public T Value { get; set; }
    
    public void Process()
    {
        if (Value is IComparable comparable)
        {
            // Boxing might occur here
            comparable.CompareTo(Value);
        }
    }
}

// With constraint - no boxing
public class Container<T> where T : IComparable<T>
{
    public T Value { get; set; }
    
    public void Process()
    {
        // No boxing - direct interface call
        Value.CompareTo(Value);
    }
}
```

**Performance Impact:**
- Boxing allocates memory on heap
- Unboxing requires type checking
- Virtual dispatch overhead
- GC pressure from allocations
- Cache misses due to heap access 