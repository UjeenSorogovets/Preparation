# Intermediate

[⬅️ Back to Table of Contents](README.md)

### 11. Explain polymorphism and its types in C#.

**Answer:** Polymorphism is a core concept in object-oriented programming (OOP) that allows objects to be treated as instances of their parent class rather than their actual derived class. This enables methods to perform different tasks based on the object that invokes them, enhancing flexibility and enabling code reusability. In C#, polymorphism can be implemented in two ways: static (compile-time) polymorphism and dynamic (runtime) polymorphism.

- **Static Polymorphism:** Achieved through method overloading and operator overloading. It allows multiple methods or operators with the same name but different parameters to coexist, with the specific method or operator being invoked determined at compile time based on the arguments passed.

- **Dynamic Polymorphism:** Achieved through method overriding. It allows a method in a derived class to have the same name and signature as a method in its base class, but with different implementation details. The method that gets executed is determined at runtime, depending on the type of the object.

Here's an example demonstrating both types of polymorphism in C#:

```csharp
// Static Polymorphism (Method Overloading)
public class Calculator
{
    public int Add(int a, int b)
    {
        return a + b;
    }

    public int Add(int a, int b, int c)
    {
        return a + b + c;
    }
}

// Dynamic Polymorphism (Method Overriding)
public class Animal
{
    public virtual void Speak()
    {
        Console.WriteLine("The animal speaks");
    }
}

public class Dog : Animal
{
    public override void Speak()
    {
        Console.WriteLine("Dog barks");
    }
}

public class Cat : Animal
{
    public override void Speak()
    {
        Console.WriteLine("Cat meows");
    }
}

// Usage
Animal animal1 = new Dog();
Animal animal2 = new Cat();

animal1.Speak(); // Output: Dog barks
animal2.Speak(); // Output: Cat meows
```

### 12. What is inheritance and how is it implemented in C#?

**Answer:** Inheritance is a fundamental concept in object-oriented programming that allows a class to inherit properties and methods from another class. The class that inherits is called the derived class or subclass, and the class from which it inherits is called the base class or superclass. Inheritance promotes code reusability and establishes a relationship between classes.

In C#, inheritance is implemented using the colon (`:`) operator. A class can inherit from only one base class (single inheritance), but it can implement multiple interfaces.

```csharp
// Base class
public class Vehicle
{
    public string Brand { get; set; }
    public string Model { get; set; }
    
    public virtual void Start()
    {
        Console.WriteLine("Vehicle is starting");
    }
}

// Derived class
public class Car : Vehicle
{
    public int NumberOfDoors { get; set; }
    
    public override void Start()
    {
        Console.WriteLine("Car is starting with engine");
    }
}

// Another derived class
public class Motorcycle : Vehicle
{
    public bool HasSidecar { get; set; }
    
    public override void Start()
    {
        Console.WriteLine("Motorcycle is starting");
    }
}

// Usage
Car car = new Car { Brand = "Toyota", Model = "Camry", NumberOfDoors = 4 };
Motorcycle motorcycle = new Motorcycle { Brand = "Honda", Model = "CBR", HasSidecar = false };

car.Start(); // Output: Car is starting with engine
motorcycle.Start(); // Output: Motorcycle is starting
```

### 13. What are interfaces and how do they differ from abstract classes?

**Answer:** Interfaces and abstract classes are both used to define contracts for classes, but they have different purposes and characteristics.

**Interfaces:**
- Define a contract that implementing classes must follow
- Can only contain method signatures, properties, events, and indexers (no implementation)
- A class can implement multiple interfaces
- Cannot contain fields or constructors
- All members are implicitly public and abstract

**Abstract Classes:**
- Can contain both abstract and concrete methods
- Can have fields, properties, and constructors
- A class can inherit from only one abstract class
- Can have access modifiers
- Can provide default implementations

```csharp
// Interface example
public interface IVehicle
{
    void Start();
    void Stop();
    string GetInfo();
}

// Abstract class example
public abstract class Vehicle
{
    public string Brand { get; set; }
    public string Model { get; set; }
    
    public abstract void Start(); // Abstract method
    
    public virtual void Stop() // Virtual method with default implementation
    {
        Console.WriteLine("Vehicle is stopping");
    }
    
    public string GetInfo() // Concrete method
    {
        return $"{Brand} {Model}";
    }
}

// Implementing both
public class Car : Vehicle, IVehicle
{
    public override void Start()
    {
        Console.WriteLine("Car is starting");
    }
    
    // IVehicle.GetInfo() is already implemented by Vehicle.GetInfo()
}
```

### 14. What are delegates and events in C#?

**Answer:** Delegates and events are mechanisms for implementing callback functionality and event-driven programming in C#.

**Delegates:**
Delegates are type-safe function pointers that can reference methods with matching signatures. They enable you to pass methods as parameters and create callback mechanisms.

```csharp
// Delegate declaration
public delegate int MathOperation(int a, int b);

// Methods that match the delegate signature
public static int Add(int a, int b) => a + b;
public static int Multiply(int a, int b) => a * b;

// Using delegates
MathOperation operation = Add;
int result = operation(5, 3); // result = 8

operation = Multiply;
result = operation(5, 3); // result = 15

// Delegates as parameters
public static int PerformOperation(int a, int b, MathOperation operation)
{
    return operation(a, b);
}

int result = PerformOperation(10, 5, Add); // result = 15
```

**Events:**
Events are a way to provide notifications when something happens. They are based on delegates and follow the publisher-subscriber pattern.

```csharp
public class Button
{
    // Event declaration
    public event EventHandler Clicked;
    
    public void Click()
    {
        // Raise the event
        Clicked?.Invoke(this, EventArgs.Empty);
    }
}

public class Program
{
    public static void Main()
    {
        Button button = new Button();
        
        // Subscribe to the event
        button.Clicked += OnButtonClicked;
        
        button.Click(); // This will trigger the event
    }
    
    private static void OnButtonClicked(object sender, EventArgs e)
    {
        Console.WriteLine("Button was clicked!");
    }
}
```

### 15. What is LINQ and how is it used?

**Answer:** LINQ (Language Integrated Query) is a set of features in C# that provides a consistent way to query data from different sources such as collections, databases, XML, and more. It allows you to write queries using a syntax similar to SQL directly in C# code.

LINQ provides two syntaxes:
1. **Query Syntax:** Similar to SQL
2. **Method Syntax:** Using extension methods

```csharp
// Sample data
var numbers = new List<int> { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
var people = new List<Person>
{
    new Person { Name = "John", Age = 25 },
    new Person { Name = "Jane", Age = 30 },
    new Person { Name = "Bob", Age = 35 }
};

// Query Syntax
var evenNumbers = from n in numbers
                  where n % 2 == 0
                  select n;

var adults = from p in people
             where p.Age >= 18
             orderby p.Name
             select p.Name;

// Method Syntax
var evenNumbers2 = numbers.Where(n => n % 2 == 0);
var adults2 = people.Where(p => p.Age >= 18)
                   .OrderBy(p => p.Name)
                   .Select(p => p.Name);

// Aggregation
var averageAge = people.Average(p => p.Age);
var oldestPerson = people.Max(p => p.Age);
var count = people.Count(p => p.Age > 25);

// Grouping
var groupedByAge = people.GroupBy(p => p.Age / 10 * 10); // Group by decade

foreach (var group in groupedByAge)
{
    Console.WriteLine($"Age group {group.Key}-{group.Key + 9}:");
    foreach (var person in group)
    {
        Console.WriteLine($"  {person.Name}");
    }
}
```

### 16. What are extension methods and how do you create them?

**Answer:** Extension methods allow you to add new methods to existing types without modifying the original type or creating a new derived type. They are static methods that are called as if they were instance methods on the extended type.

Extension methods must be defined in a static class and the first parameter must be the type being extended, preceded by the `this` keyword.

```csharp
// Extension method for string
public static class StringExtensions
{
    public static string Reverse(this string str)
    {
        char[] chars = str.ToCharArray();
        Array.Reverse(chars);
        return new string(chars);
    }
    
    public static bool IsPalindrome(this string str)
    {
        string cleaned = str.ToLower().Replace(" ", "");
        return cleaned == cleaned.Reverse();
    }
    
    public static string ToTitleCase(this string str)
    {
        if (string.IsNullOrEmpty(str))
            return str;
            
        return char.ToUpper(str[0]) + str.Substring(1).ToLower();
    }
}

// Extension method for IEnumerable<T>
public static class EnumerableExtensions
{
    public static IEnumerable<T> Shuffle<T>(this IEnumerable<T> source)
    {
        var random = new Random();
        return source.OrderBy(x => random.Next());
    }
    
    public static string ToDelimitedString<T>(this IEnumerable<T> source, string delimiter = ", ")
    {
        return string.Join(delimiter, source);
    }
}

// Usage
string text = "hello world";
Console.WriteLine(text.Reverse()); // "dlrow olleh"
Console.WriteLine(text.ToTitleCase()); // "Hello world"
Console.WriteLine("racecar".IsPalindrome()); // true

var numbers = new List<int> { 1, 2, 3, 4, 5 };
var shuffled = numbers.Shuffle();
Console.WriteLine(numbers.ToDelimitedString()); // "1, 2, 3, 4, 5"
```

### 17. What is the difference between IEnumerable, ICollection, and IList?

**Answer:** These are different interfaces in the .NET collection hierarchy, each providing different levels of functionality:

**IEnumerable<T>:**
- Most basic interface
- Provides read-only, forward-only access to elements
- Supports foreach iteration
- Cannot modify the collection

**ICollection<T>:**
- Extends IEnumerable<T>
- Adds methods to modify the collection (Add, Remove, Clear)
- Provides Count property
- Does not support indexing

**IList<T>:**
- Extends ICollection<T>
- Adds indexing support (this[int index])
- Supports Insert, RemoveAt, IndexOf methods
- Allows random access to elements

```csharp
// IEnumerable - read-only iteration
IEnumerable<int> numbers = new List<int> { 1, 2, 3, 4, 5 };
foreach (int num in numbers)
{
    Console.WriteLine(num);
}

// ICollection - can modify collection
ICollection<int> collection = new List<int> { 1, 2, 3 };
collection.Add(4);
collection.Remove(2);
Console.WriteLine(collection.Count); // 3

// IList - supports indexing
IList<int> list = new List<int> { 1, 2, 3, 4, 5 };
int first = list[0]; // Access by index
list[1] = 10; // Modify by index
list.Insert(2, 15); // Insert at specific position
int index = list.IndexOf(4); // Find index of element
```

### 18. What is the difference between var and dynamic in C#?

**Answer:** Both `var` and `dynamic` are used for type inference, but they work very differently:

**var:**
- Compile-time type inference
- The type is determined at compile time and cannot be changed
- Provides IntelliSense and compile-time type checking
- Better performance as no runtime type checking is needed

**dynamic:**
- Runtime type inference
- Type checking is deferred until runtime
- No IntelliSense support
- Slower performance due to runtime type checking
- Can change the type of the variable at runtime

```csharp
// var - compile-time type inference
var number = 42; // int
var text = "Hello"; // string
var list = new List<int>(); // List<int>

// These would cause compile-time errors:
// number = "string"; // Error: cannot convert string to int
// text = 123; // Error: cannot convert int to string

// dynamic - runtime type inference
dynamic value = 42;
Console.WriteLine(value); // 42

value = "Hello"; // Can change type at runtime
Console.WriteLine(value); // Hello

value = new List<int> { 1, 2, 3 };
Console.WriteLine(value.Count); // 3

// Runtime errors are possible with dynamic
try
{
    dynamic obj = "string";
    int result = obj + 5; // Runtime error: cannot add string and int
}
catch (RuntimeBinderException ex)
{
    Console.WriteLine("Runtime error: " + ex.Message);
}
```

### 19. What are async and await keywords in C#?

**Answer:** `async` and `await` are keywords used for asynchronous programming in C#. They allow you to write asynchronous code that looks similar to synchronous code, making it easier to handle long-running operations without blocking the main thread.

**async:**
- Marks a method as asynchronous
- The method can contain await expressions
- Returns a Task, Task<T>, or void

**await:**
- Pauses execution of the async method until the awaited task completes
- Returns control to the caller
- Can only be used inside async methods

```csharp
// Synchronous method
public string GetData()
{
    // This blocks the thread
    Thread.Sleep(2000);
    return "Data";
}

// Asynchronous method
public async Task<string> GetDataAsync()
{
    // This doesn't block the thread
    await Task.Delay(2000);
    return "Data";
}

// Using async/await
public async Task ProcessDataAsync()
{
    Console.WriteLine("Starting...");
    
    // This doesn't block the UI thread
    string data = await GetDataAsync();
    
    Console.WriteLine("Received: " + data);
}

// Multiple async operations
public async Task ProcessMultipleAsync()
{
    var task1 = GetDataAsync();
    var task2 = GetDataAsync();
    
    // Wait for both to complete
    var results = await Task.WhenAll(task1, task2);
    
    Console.WriteLine($"Result 1: {results[0]}");
    Console.WriteLine($"Result 2: {results[1]}");
}

// Error handling in async methods
public async Task<string> GetDataWithErrorHandlingAsync()
{
    try
    {
        await Task.Delay(2000);
        return "Data";
    }
    catch (Exception ex)
    {
        Console.WriteLine($"Error: {ex.Message}");
        return null;
    }
}
```

### 20. What is the difference between Task and ValueTask?

**Answer:** Both `Task` and `ValueTask` represent asynchronous operations, but they have different performance characteristics and use cases:

**Task:**
- Reference type (allocated on heap)
- Good for operations that are likely to be asynchronous
- More overhead due to heap allocation
- Can be awaited multiple times

**ValueTask:**
- Value type (allocated on stack when possible)
- Better performance for operations that are likely to complete synchronously
- Cannot be awaited multiple times
- Introduced in .NET Core 2.1

```csharp
// Task example
public async Task<string> GetDataTaskAsync()
{
    await Task.Delay(100);
    return "Data from Task";
}

// ValueTask example
public async ValueTask<string> GetDataValueTaskAsync()
{
    // If the operation completes synchronously, no heap allocation
    if (IsDataAvailable())
    {
        return "Data from ValueTask (synchronous)";
    }
    
    // Only allocate if truly asynchronous
    await Task.Delay(100);
    return "Data from ValueTask (asynchronous)";
}

// Usage
public async Task ProcessDataAsync()
{
    var taskResult = await GetDataTaskAsync();
    var valueTaskResult = await GetDataValueTaskAsync();
    
    Console.WriteLine(taskResult);
    Console.WriteLine(valueTaskResult);
}

// When to use ValueTask
public async ValueTask<int> GetCachedValueAsync(int key)
{
    // Check cache first (likely synchronous)
    if (_cache.TryGetValue(key, out int value))
    {
        return value; // No heap allocation
    }
    
    // Only go async if not in cache
    value = await FetchFromDatabaseAsync(key);
    _cache[key] = value;
    return value;
}
``` 