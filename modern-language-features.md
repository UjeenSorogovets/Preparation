# Modern Language Features

[⬅️ Back to Table of Contents](README.md)

### 31. What are generic constraints and why do they matter?

**Answer:** Generic constraints (where T : class, struct, new(), interface, unmanaged) let the compiler assume specific capabilities of T, enable efficient code-gen (no boxing for constrained value types) and improve overload resolution. They act on the use-site of a generic and are enforced at compile time and again by the CLR verifier at JIT time.

**Example:**
```csharp
// Without constraint - limited operations
public class Container<T>
{
    public T Value { get; set; }
    // Can't call methods on T without knowing its capabilities
}

// With constraint - can use specific capabilities
public class Container<T> where T : class, new()
{
    public T Value { get; set; }
    
    public Container()
    {
        Value = new T(); // Can create new instance
    }
    
    public bool IsNull() => Value == null; // Can compare to null
}
```

**Common Constraints:**
- `where T : class` - T must be a reference type
- `where T : struct` - T must be a value type
- `where T : new()` - T must have a parameterless constructor
- `where T : IComparable` - T must implement IComparable
- `where T : unmanaged` - T must be an unmanaged type

### 32. Explain covariance and contravariance in C#.

**Answer:** Variance allows implicit reference-conversion for generic parameters marked out (covariant, read-only position) or in (contravariant, write-only position). For example, IEnumerable<object> can reference an IEnumerable<string> but the reverse is illegal. This relies on runtime type-safety checks performed by the CLR for delegates and interfaces.

**Covariance (out):**
```csharp
// Covariant interface - can assign more derived to less derived
public interface IProducer<out T>
{
    T GetItem();
}

// This works because string is derived from object
IProducer<string> stringProducer = new StringProducer();
IProducer<object> objectProducer = stringProducer; // Covariant assignment
```

**Contravariance (in):**
```csharp
// Contravariant interface - can assign less derived to more derived
public interface IConsumer<in T>
{
    void Consume(T item);
}

// This works because we can pass object to a method expecting string
IConsumer<object> objectConsumer = new ObjectConsumer();
IConsumer<string> stringConsumer = objectConsumer; // Contravariant assignment
```

### 33. Why were records introduced and when should you prefer them to classes?

**Answer:** record (class/struct) gives value-based equality, an auto-generated Deconstruct, non-destructive with updates and a default immutable design. They reduce boilerplate in DTOs, commands and events where identity is defined by contained data rather than by reference.

**Example:**
```csharp
// Traditional class approach
public class Person
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    
    public override bool Equals(object obj)
    {
        return obj is Person person &&
               FirstName == person.FirstName &&
               LastName == person.LastName;
    }
    
    public override int GetHashCode()
    {
        return HashCode.Combine(FirstName, LastName);
    }
}

// Record approach - much simpler
public record Person(string FirstName, string LastName);

// Usage
var person1 = new Person("John", "Doe");
var person2 = new Person("John", "Doe");
Console.WriteLine(person1 == person2); // True - value-based equality

// Non-destructive update
var person3 = person1 with { LastName = "Smith" };
```

**When to use records:**
- DTOs (Data Transfer Objects)
- Configuration objects
- Immutable data structures
- Value objects in domain-driven design

### 34. What does modern pattern matching add over classic switch?

**Answer:** Relational (>, <), property and positional patterns plus logical combinators (and, or, not) let you express complex branching declaratively. The compiler enforces exhaustiveness for switch expressions and emits minimal IL with no boxing or hidden allocations.

**Classic switch:**
```csharp
switch (shape)
{
    case Circle c:
        return Math.PI * c.Radius * c.Radius;
    case Rectangle r:
        return r.Width * r.Height;
    default:
        throw new ArgumentException("Unknown shape");
}
```

**Modern pattern matching:**
```csharp
// Property patterns
var area = shape switch
{
    Circle { Radius: > 0 } c => Math.PI * c.Radius * c.Radius,
    Rectangle { Width: > 0, Height: > 0 } r => r.Width * r.Height,
    Triangle { Base: > 0, Height: > 0 } t => 0.5 * t.Base * t.Height,
    _ => throw new ArgumentException("Invalid shape")
};

// Positional patterns with deconstruction
var result = point switch
{
    (0, 0) => "Origin",
    (_, 0) => "X-axis",
    (0, _) => "Y-axis",
    (var x, var y) when x > 0 && y > 0 => "First quadrant",
    _ => "Other"
};
```

### 35. Describe nullable reference types.

**Answer:** By enabling #nullable enable, every reference splits into string (non-null) or string? (may be null). The static flow-analysis engine issues CS8602/CS8600 warnings where a possible null is dereferenced or where null is assigned to a non-nullable slot, cutting most NullReferenceExceptions before runtime.

**Example:**
```csharp
#nullable enable

public class Person
{
    public string Name { get; set; } = string.Empty; // Non-nullable
    public string? Email { get; set; } // Nullable
    
    public void ProcessName()
    {
        // No warning - Name is guaranteed non-null
        Console.WriteLine(Name.Length);
        
        // Warning CS8602 - possible null reference
        Console.WriteLine(Email.Length);
        
        // Safe - null check
        if (Email != null)
        {
            Console.WriteLine(Email.Length); // No warning
        }
        
        // Safe - null-forgiving operator
        Console.WriteLine(Email!.Length); // Suppresses warning
    }
}
```

**Benefits:**
- Catches null reference bugs at compile time
- Makes intent explicit in code
- Improves code documentation
- Reduces runtime exceptions

### 36. When would you use Span<T> / Memory<T>?

**Answer:** They are stack-only (ref struct) types that provide safe, slicing views over contiguous memory (arrays, stackalloc, unmanaged buffers). Because they avoid heap allocations and copy-on-access, they're ideal for parsers, high-throughput I/O and hot JSON decoding.

**Example:**
```csharp
// Traditional approach - allocates new string
public string ReverseString(string input)
{
    char[] chars = input.ToCharArray();
    Array.Reverse(chars);
    return new string(chars);
}

// Span<T> approach - no allocations
public string ReverseStringSpan(string input)
{
    Span<char> chars = stackalloc char[input.Length];
    input.CopyTo(chars);
    chars.Reverse();
    return new string(chars);
}

// Parsing with Span<T>
public int ParseInt(ReadOnlySpan<char> input)
{
    int result = 0;
    for (int i = 0; i < input.Length; i++)
    {
        if (char.IsDigit(input[i]))
        {
            result = result * 10 + (input[i] - '0');
        }
    }
    return result;
}
```

**Use cases:**
- High-performance parsing
- JSON/XML processing
- Network I/O operations
- Memory-efficient string operations 