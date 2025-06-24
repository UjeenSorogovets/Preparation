# .NET (C#) Interview Questions and Answers

This document contains a collection of 70+ interview questions related to .NET and the C# programming language, aimed at assessing candidates at various levels of expertise.

## Basic

1. **What is .NET?**
2. **Can you explain the Common Language Runtime (CLR)?**
3. **What is the difference between managed and unmanaged code?**
4. **Explain the basic structure of a C# program.**
5. **What are Value Types and Reference Types in C#?**
6. **What is garbage collection in .NET?**
7. **Explain the concept of exception handling in C#.**
8. **What are the different types of classes in C#?**
9. **Can you describe what a namespace is and how it is used in C#?**
10. **What is encapsulation?**

## Intermediate

11. **Explain polymorphism and its types in C#.**
12. **What are delegates and how are they used in C#?**
13. **Describe what LINQ is and give an example of where it might be used.**
14. **What is the difference between an abstract class and an interface?**
15. **How do you manage memory in .NET applications?**
16. **Explain the concept of threading in .NET.**
17. **What is async/await and how does it work?**
18. **Describe the Entity Framework and its advantages.**
19. **What are extension methods and where would you use them?**
20. **How do you handle exceptions in a method that returns a Task?**

## Advanced

21. **What is reflection in .NET and how would you use it?**
22. **Can you explain the concept of middleware in ASP.NET Core?**
23. **Describe the Dependency Injection (DI) pattern and how it's implemented in .NET Core.**
24. **What is the purpose of the .NET Standard?**
25. **Explain the differences between .NET Core, .NET Framework, and Xamarin.**
26. **How does garbage collection work in .NET and how can you optimize it?**
27. **What are attributes in C# and how can they be used?**
28. **Can you describe the process of code compilation in .NET?**
29. **What is the Global Assembly Cache (GAC) and when should it be used?**
30. **How would you secure a web application in ASP.NET Core?**

## Modern Language Features

31. **What are generic constraints and why do they matter?**
32. **Explain covariance and contravariance in C#.**
33. **Why were records introduced and when should you prefer them to classes?**
34. **What does modern pattern matching add over classic switch?**
35. **Describe nullable reference types.**
36. **When would you use Span<T> / Memory<T>?**

## Performance and Memory

37. **How do GC generations and the Large Object Heap work?**
38. **Name typical managed-memory leaks in long-running services.**
39. **Why is boxing/unboxing often highlighted in performance reviews?**

## Async & Concurrency

40. **What does ConfigureAwait(false) actually do?**
41. **Benefits of IAsyncEnumerable<T> and await foreach.**
42. **Why was IAsyncDisposable added?**

## Architecture & Patterns

43. **Illustrate SOLID with dependency injection in .NET.**
44. **When and how to use Repository + Unit of Work with EF Core?**
45. **Outline Clean Architecture layers.**

## Framework-Specific

46. **What is MVC (Model-View-Controller)?**
47. **Can you explain the difference between Razor Pages and MVC in ASP.NET Core?**
48. **How do you perform validations in ASP.NET Core?**
49. **Describe SignalR and its use cases.**
50. **What are the benefits of using Blazor over traditional web technologies?**
51. **How do you implement Web API versioning in ASP.NET Core?**
52. **Explain the role of IApplicationBuilder in ASP.NET Core.**
53. **What are Areas in ASP.NET Core and how do you use them?**
54. **How do you manage sessions in ASP.NET Core applications?**
55. **Describe how to implement caching in ASP.NET Core.**
56. **Minimal APIs vs. MVC controllers in ASP.NET Core 8.**
57. **Why is middleware order critical?**
58. **How do you secure an API with JWT in ASP.NET Core?**

## Testing & Best Practices

59. **What is Unit Testing in .NET?**
60. **How do you mock dependencies in unit tests using .NET?**
61. **Can you explain SOLID principles?**
62. **What is Continuous Integration/Continuous Deployment (CI/CD) and how does it apply to .NET development?**
63. **How do you ensure your C# code is secure?**
64. **What are some common performance issues in .NET applications and how do you address them?**
65. **Describe the Repository pattern and its benefits.**
66. **How do you handle database migrations in Entity Framework?**
67. **What tools do you use for debugging and profiling .NET applications?**
68. **How do you stay updated with the latest .NET technologies and practices?**
69. **How do xUnit and Moq work together in unit tests?**
70. **Purpose of WebApplicationFactory in integration tests.**
71. **What does dotnet publish single-file/self-contained achieve?**

## SQL
72. **What is the difference between INNER JOIN, LEFT JOIN, RIGHT JOIN, and FULL JOIN?**  
73. **What is a primary key and how does it differ from a unique key?**  
74. **What are foreign keys and how do they enforce referential integrity?**  
75. **Explain normalization and list the different normal forms.**  
76. **What is a clustered index vs a non-clustered index?**  
77. **What are transactions in SQL and what are ACID properties?**  
78. **What is the difference between DELETE, TRUNCATE, and DROP?**  
79. **What are window functions in SQL and when would you use them?**  
80. **How does a Common Table Expression (CTE) work and how is it different from a subquery?**  
81. **What are the advantages and disadvantages of using stored procedures?**  
82. **How can you detect and prevent SQL injection?**  
83. **What is the difference between EXISTS and IN operators in SQL?**  
84. **How does indexing work and how can you identify slow queries?**  
85. **What is the use of the `EXPLAIN` or `QUERY PLAN` statement?**  
86. **What are aggregate functions and how are GROUP BY and HAVING used?**  
87. **What is a composite key and when should it be used?**  
88. **What is a materialized view and how does it differ from a regular view?**  
89. **How do you handle NULL values in queries and constraints?**  
90. **What is the difference between scalar functions and table-valued functions?**  
91. **How would you design a schema for a multi-tenant application in SQL?**  

    
## Basic

### 1. What is .NET?

**Answer:** .NET is a comprehensive development platform used for building a wide variety of applications, including web, mobile, desktop, and gaming. It supports multiple programming languages, such as C#, F#, and Visual Basic. .NET provides a large class library called Framework Class Library (FCL) and runs on a Common Language Runtime (CLR) which offers services like memory management, security, and exception handling.

### 2. Can you explain the Common Language Runtime (CLR)?

**Answer:** The CLR is a virtual machine component of the .NET framework that manages the execution of .NET programs. It provides important services such as memory management, type safety, exception handling, garbage collection, and thread management. The CLR converts Intermediate Language (IL) code into native machine code through a process called Just-In-Time (JIT) compilation. This ensures that .NET applications can run on any device or platform that supports the .NET framework.

### 3. What is the difference between managed and unmanaged code?

**Answer:** Managed code is executed by the CLR, which provides services like garbage collection, exception handling, and type checking. It's called "managed" because the CLR manages a lot of the functionalities that developers would otherwise need to implement themselves. Unmanaged code, on the other hand, is executed directly by the operating system, and all memory allocation, type safety, and security must be handled by the programmer. Examples of unmanaged code include applications written in C or C++.

### 4. Explain the basic structure of a C# program.

**Answer:** A basic C# program consists of the following elements:

- **Namespace declaration:** A way to organize code and control the scope of classes and methods in larger projects.
- **Class declaration:** Defines a new type with data members (fields, properties) and function members (methods, constructors).
- **Main method:** The entry point for the program where execution begins and ends.
- **Statements and expressions:** Perform actions with variables, calling methods, looping through collections, etc.

```csharp
using System;

namespace HelloWorld
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```

### 5. What are Value Types and Reference Types in C#?

**Answer:** In C#, data types are divided into two categories: Value Types and Reference Types. This distinction affects how values are stored and manipulated within memory.

- **Value Types:** Store data directly and are allocated on the stack. This means that when you assign one value type to another, a direct copy of the value is created. Basic data types (`int`, `double`, `bool`, etc.) and structs are examples of value types. Operations on value types are generally faster due to stack allocation.

- **Reference Types:** Store a reference (or pointer) to the actual data, which is allocated on the heap. When you assign one reference type to another, both refer to the same object in memory; changes made through one reference are reflected in the other. Classes, arrays, delegates, and strings are examples of reference types.

Here's a simple example to illustrate the difference:

```csharp
// Value type example
int a = 10;
int b = a;
b = 20;
Console.WriteLine(a); // Output: 10
Console.WriteLine(b); // Output: 20

// Reference type example
var list1 = new List<int> { 1, 2, 3 };
var list2 = list1;
list2.Add(4);
Console.WriteLine(list1.Count); // Output: 4
Console.WriteLine(list2.Count); // Output: 4
```

In the value type example, changing b does not affect a because b is a separate copy. In the reference type example, list2 is not a separate copy; it's another reference to the same list object as list1, so changes made through list2 are visible when accessing list1.

### 6. What is garbage collection in .NET?

**Answer:** Garbage collection (GC) in .NET is an automatic memory management feature that frees up memory used by objects that are no longer accessible in the program. It eliminates the need for developers to manually release memory, thereby reducing memory leaks and other memory-related errors. The GC operates on a separate thread and works in three phases: marking, relocating, and compacting. During the marking phase, it identifies which objects in the heap are still in use. During the relocating phase, it updates the references to objects that will be compacted. Finally, during the compacting phase, it reclaims the space occupied by the garbage objects and compacts the remaining objects to make memory allocation more efficient.

### 7. Explain the concept of exception handling in C#.

**Answer:** Exception handling in C# is a mechanism to handle runtime errors, allowing a program to continue running or fail gracefully instead of crashing. It is done using the try, catch, and finally blocks. The try block contains code that might throw an exception, while catch blocks are used to handle the exception. The finally block contains code that is executed whether an exception is thrown or not, often for cleanup purposes.

```csharp
try {
    // Code that may cause an exception
    int divide = 10 / 0;
}
catch (DivideByZeroException ex) {
    // Code to handle the exception
    Console.WriteLine("Cannot divide by zero. Please try again.");
}
finally {
    // Code that executes after try/catch, regardless of an exception
    Console.WriteLine("Operation completed.");
}
```

### 8. What are the different types of classes in C#?

**Answer:** In C#, classes can be categorized based on their functionality and accessibility:

- **Static classes:** Cannot be instantiated and can only contain static members.
- **Sealed classes:** Cannot be inherited from.
- **Abstract classes:** Cannot be instantiated and are meant to be inherited from.
- **Partial classes:** Allow the splitting of a class definition across multiple files.
- **Generic classes:** Allow the definition of classes with placeholders for the type of its fields, methods, parameters, etc.

Each type serves different purposes in the context of object-oriented programming and design patterns.

### 9. Can you describe what a namespace is and how it is used in C#?

**Answer:** A namespace in C# is used to organize code into a hierarchical structure. It allows the grouping of logically related classes, structs, interfaces, enums, and delegates. Namespaces help avoid naming conflicts by qualifying the uniqueness of each type. For example, the `System` namespace in .NET includes classes for basic system operations, such as console input/output, file reading/writing, and data manipulation.

```csharp
using System;

namespace MyApplication
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello, World!");
        }
    }
}
```

In this example, the System namespace is used to access the Console class, and MyApplication is a custom namespace for organizing the application's code. Namespaces are essential for managing the scope of names in larger programming projects to avoid name collisions.

### 10. What is encapsulation?

**Answer:** Encapsulation is a fundamental principle of object-oriented programming (OOP) that involves bundling the data (attributes) and methods (operations) that operate on the data into a single unit, or class, and restricting access to the internals of that class. This is typically achieved through the use of access modifiers such as `private`, `public`, `protected`, and `internal`. Encapsulation helps to protect an object's internal state from unauthorized access and modification by external code, promoting data integrity and security.

Encapsulation allows the internal representation of an object to be hidden from the outside, only allowing access through a public interface. This concept is also known as data hiding. By controlling how data is accessed and modified, encapsulation helps to reduce complexity and increase reusability of code.

Here is a simple example demonstrating encapsulation in C#:

```csharp
public class Person
{
    private string name; // Private field, encapsulated data

    public string Name // Public property, access to the name field
    {
        get { return name; }
        set { name = value; }
    }

    public Person(string name) // Constructor
    {
        this.name = name;
    }
}

class Program
{
    static void Main(string[] args)
    {
        Person person = new Person("John");
        Console.WriteLine(person.Name); // Accessing name through a public property
    }
}
```

In this example, the name field of the Person class is encapsulated and only accessible via the Name property. This approach allows the Person class to control how the name field is accessed and modified, ensuring that any rules or validations about the data can be applied within the class itself.

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

class Program
{
    static void Main(string[] args)
    {
        Calculator calc = new Calculator();
        Console.WriteLine(calc.Add(2, 3)); // Calls the first Add method
        Console.WriteLine(calc.Add(2, 3, 4)); // Calls the second Add method

        Animal myAnimal = new Animal();
        myAnimal.Speak(); // Output: The animal speaks

        Dog myDog = new Dog();
        myDog.Speak(); // Output: Dog barks

        Animal mySecondAnimal = new Dog();
        mySecondAnimal.Speak(); // Output: Dog barks, demonstrating dynamic polymorphism
    }
}
```

In the example above, the Calculator class demonstrates static polymorphism through method overloading, allowing the Add method to be called with different numbers of parameters. The Animal and Dog classes illustrate dynamic polymorphism, where the Speak method in the Dog class overrides the Speak method in its base class, Animal. The type of polymorphism used depends on the object reference at runtime, showcasing polymorphism's flexibility in OOP.

### 12. What are delegates and how are they used in C#?

**Answer:** Delegates in C# are type-safe function pointers or references to methods with a specific parameter list and return type. They allow methods to be passed as parameters, stored in variables, and returned by other methods, which enables flexible and extensible programming designs such as event handling and callback methods. Delegates are particularly useful in implementing the observer pattern and designing frameworks or components that need to notify other objects about events or changes without knowing the specifics of those objects.

There are three main types of delegates in C#:
- **Single-cast delegates:** Point to a single method at a time.
- **Multicast delegates:** Can point to multiple methods on a single invocation list.
- **Anonymous methods/Lambda expressions:** Allow inline methods or lambda expressions to be used wherever a delegate is expected.

Here is an example demonstrating the use of delegates in C#:

```csharp
public delegate void Operation(int num);

class Program
{
    static void Main(string[] args)
    {
        Operation op = Double;
        op(5);  // Output: 10

        op = Triple;
        op(5);  // Output: 15

        // Multicast delegate
        op = Double;
        op += Triple; // Combines Double and Triple methods
        op(5);  // Output: 10 followed by 15
    }

    static void Double(int num)
    {
        Console.WriteLine($"{num} * 2 = {num * 2}");
    }

    static void Triple(int num)
    {
        Console.WriteLine($"{num} * 3 = {num * 3}");
    }
}
```

In this example, the Operation delegate is defined to point to any method that accepts an int and returns void. Initially, op is set to the Double method, demonstrating a single-cast delegate. It is then reassigned to the Triple method, and finally, it is used as a multicast delegate to call both Double and Triple methods in sequence. This demonstrates how delegates in C# provide a flexible mechanism for method invocation and can be used to implement event handlers and callbacks.

### 13. Describe what LINQ is and give an example of where it might be used.

**Answer:** LINQ (Language Integrated Query) is a powerful feature in C# that allows developers to write expressive, readable code to query and manipulate data. It provides a uniform way to query various data sources, such as collections in memory, databases (via LINQ to SQL, LINQ to Entities), XML documents (LINQ to XML), and more. LINQ queries offer three main benefits: they are strongly typed, offer compile-time checking, and support IntelliSense, which enhances developer productivity and code maintainability.

LINQ can be used in a variety of scenarios, including filtering, sorting, and grouping data. It supports both method syntax and query syntax, providing flexibility in how queries are expressed.

Here is a simple example demonstrating LINQ with a list of integers:

```csharp
using System;
using System.Linq;
using System.Collections.Generic;

class Program
{
    static void Main(string[] args)
    {
        List<int> numbers = new List<int> { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

        // Use LINQ to find all even numbers
        var evenNumbers = from num in numbers
                          where num % 2 == 0
                          select num;

        Console.WriteLine("Even numbers:");
        foreach (var num in evenNumbers)
        {
            Console.WriteLine(num);
        }
    }
}
```

In this example, a LINQ query is used to filter a list of integers, selecting only the even numbers. The query is expressed using LINQ's query syntax, which closely resembles SQL in its readability and structure. This demonstrates how LINQ makes it easier to work with collections and other data sources by abstracting the complexity of different data manipulation operations.

### 14. What is the difference between an abstract class and an interface?

**Answer:** In C#, both abstract classes and interfaces are types that enable polymorphism, allowing objects of different classes to be treated as objects of a common super class. However, they serve different purposes and have different rules:

- **Abstract Class:**
  - Can contain implementation of methods, properties, fields, or events.
  - Can have access modifiers (public, protected, etc.).
  - A class can inherit from only one abstract class (single inheritance).
  - Can contain constructors.
  - Used when different implementations of objects have common methods or properties that can share a common implementation.

- **Interface:**
  - Cannot contain implementations, only declarations of methods, properties, events, or indexers.
  - Members of an interface are implicitly public.
  - A class or struct can implement multiple interfaces (multiple inheritance).
  - Cannot contain fields or constructors.
  - Used to define a contract for classes without imposing inheritance hierarchies.

Here is an example illustrating the use of an abstract class and an interface:

```csharp
public abstract class Animal
{
    public abstract void Eat();
    public void Sleep()
    {
        Console.WriteLine("Sleeping");
    }
}

public interface IMovable
{
    void Move();
}

public class Dog : Animal, IMovable
{
    public override void Eat()
    {
        Console.WriteLine("Dog is eating");
    }

    public void Move()
    {
        Console.WriteLine("Dog is running");
    }
}

class Program
{
    static void Main(string[] args)
    {
        Dog myDog = new Dog();
        myDog.Eat();
        myDog.Sleep();
        myDog.Move();
    }
}
```

In this example, Animal is an abstract class that provides a default implementation of the Sleep method and an abstract Eat method that must be overridden. IMovable is an interface that defines a contract with a Move method that must be implemented. Dog inherits from Animal and implements IMovable, thereby fulfilling both the contract defined by the interface and extending the functionality provided by the abstract class.

### 15. How do you manage memory in .NET applications?

**Answer:** Memory management in .NET applications is primarily handled automatically by the Garbage Collector (GC), which provides a high-level abstraction for memory allocation and deallocation, ensuring that developers do not need to manually free memory. However, understanding and cooperating with the GC can help improve your application's performance and memory usage. Here are key aspects of memory management in .NET:

- **Garbage Collection:** Automatically reclaims memory occupied by unreachable objects, freeing developers from manually deallocating memory and helping to avoid memory leaks.

- **Dispose Pattern:** Implementing the `IDisposable` interface and the `Dispose` method allows for the cleanup of unmanaged resources (such as file handles, database connections, etc.) that the GC cannot reclaim automatically.

- **Finalizers:** Can be defined in classes to perform cleanup operations before the object is collected by the GC. However, overuse of finalizers can negatively impact performance, as it makes objects live longer than necessary.

- **Using Statements:** A syntactic sugar for calling `Dispose` on IDisposable objects, ensuring that resources are freed as soon as they are no longer needed, even if exceptions are thrown.

- **Large Object Heap (LOH) Management:** Large objects are allocated on a separate heap, and knowing how to manage large object allocations can help reduce memory fragmentation and improve performance.

Here is an example demonstrating the use of the `IDisposable` interface and `using` statement for resource management:

```csharp
public class ResourceHolder : IDisposable
{
    private bool disposed = false;

    // Simulate an unmanaged resource.
    IntPtr unmanagedResource = Marshal.AllocHGlobal(100);

    public void Dispose()
    {
        Dispose(true);
        GC.SuppressFinalize(this);
    }

    protected virtual void Dispose(bool disposing)
    {
        if (!disposed)
        {
            if (disposing)
            {
                // Dispose managed resources.
            }

            // Free unmanaged resources
            Marshal.FreeHGlobal(unmanagedResource);
            disposed = true;
        }
    }

    ~ResourceHolder()
    {
        Dispose(false);
    }
}

class Program
{
    static void Main(string[] args)
    {
        using (ResourceHolder holder = new ResourceHolder())
        {
            // Use the resource
        } // Automatic disposal here
    }
}
```

In this example, ResourceHolder implements IDisposable to properly manage both managed and unmanaged resources. The using statement ensures that Dispose is called automatically, providing a robust pattern for resource management in .NET applications.

### 16. Explain the concept of threading in .NET.

**Answer:** Threading in .NET allows for the execution of multiple operations simultaneously within the same process. It enables applications to perform background tasks, UI responsiveness, and parallel computations, improving overall application performance and efficiency. The .NET framework provides several ways to create and manage threads:

- **System.Threading.Thread:** A low-level approach to create and manage threads directly. This class offers fine-grained control over thread behavior.

- **ThreadPool:** A collection of worker threads maintained by the .NET runtime, offering efficient execution of short-lived background tasks without the overhead of creating individual threads for each task.

- **Task Parallel Library (TPL):** Provides a higher-level abstraction over threading, using tasks that represent asynchronous operations. TPL uses the ThreadPool internally and supports features like task chaining, cancellation, and continuation.

- **async and await:** Keywords that simplify asynchronous programming, making it easier to write asynchronous code that's as straightforward as synchronous code.

Here is an example demonstrating the use of the `System.Threading.Thread` class:

```csharp
using System;
using System.Threading;

class Program
{
    static void Main(string[] args)
    {
        Thread thread = new Thread(new ThreadStart(DoWork));
        thread.Start();

        Console.WriteLine("Main thread does some work, then waits.");
        thread.Join();
        Console.WriteLine("Background thread has completed. Main thread ends.");
    }

    static void DoWork()
    {
        Console.WriteLine("Background thread is working.");
        Thread.Sleep(1000); // Simulates doing work
        Console.WriteLine("Background thread has finished.");
    }
}
```

In this example, a new thread is created and started to execute the DoWork method in parallel to the main thread. The main thread then waits for the background thread to complete using the Join method before it proceeds to finish. This demonstrates the basic use of threading to perform operations concurrently.

Using threads can significantly improve the responsiveness and performance of your application but also introduces complexity, such as the need for thread synchronization to avoid race conditions and deadlocks. Proper understanding and careful management are essential when working with threads in .NET.

### 17. What is async/await and how does it work?

**Answer:** In C#, `async` and `await` are keywords that simplify writing asynchronous code, making it more readable and maintainable. This feature allows developers to perform non-blocking operations without the complex code traditionally associated with asynchronous programming, such as callbacks or manual thread management. The `async` modifier indicates that a method is asynchronous and may contain one or more `await` expressions. The `await` keyword is applied to a task, indicating that the method should pause until the awaited task completes, allowing other operations to run concurrently without blocking the main thread.

Key points about async/await:
- Improves application responsiveness, particularly important for UI applications where long-running operations can freeze the user interface.
- Enables server applications to handle more concurrent requests by freeing up threads while waiting for operations to complete.
- Simplifies error handling in asynchronous code with try-catch blocks.

Here's a simple example demonstrating async/await:

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;

class Program
{
    static async Task Main(string[] args)
    {
        string result = await DownloadContentAsync();
        Console.WriteLine(result);
    }

    static async Task<string> DownloadContentAsync()
    {
        using HttpClient client = new HttpClient();
        string result = await client.GetStringAsync("http://example.com");
        return result;
    }
}
```

In this example, DownloadContentAsync is an asynchronous method that downloads content from a web address. It uses await to asynchronously wait for the HTTP request to complete without blocking the main thread. The Main method is also marked with async and awaits the completion of DownloadContentAsync. This approach keeps the application responsive, as the thread that started the operation can perform other work while waiting for the HTTP request to complete.

Async/await simplifies asynchronous programming by allowing developers to write code that's both easy to read and maintain, resembling synchronous code while providing the benefits of asynchronous execution.

### 18. Describe the Entity Framework and its advantages.

**Answer:** Entity Framework (EF) is an open-source object-relational mapping (ORM) framework for .NET. It enables developers to work with databases using .NET objects, eliminating the need for most of the data-access code that developers usually need to write. Entity Framework provides a high-level abstraction over database connections and operations, allowing developers to perform CRUD (Create, Read, Update, Delete) operations without having to deal with the underlying database SQL commands directly.

Advantages of using Entity Framework include:
- **Increased Productivity:** Automatically generates classes based on database schemas, reducing the amount of manual coding required for data access.
- **Maintainability:** Changes to the database schema can be easily propagated to the code through migrations, helping maintain code and database schema synchronicity.
- **Support for LINQ:** Enables developers to use LINQ queries to access and manipulate data, providing a type-safe way to query databases that integrates with the C# language.
- **Database Agnostic:** EF can work with various databases, including SQL Server, MySQL, Oracle, and more, by changing the database provider with minimal changes to the code.
- **Caching, Lazy Loading, Eager Loading:** Offers built-in support for caching, and configurable loading options like lazy loading and eager loading, improving application performance.

Here is a simple example demonstrating the use of Entity Framework to query a database:

```csharp
using System;
using System.Linq;
using System.Data.Entity;

public class BloggingContext : DbContext
{
    public DbSet<Blog> Blogs { get; set; }
}

public class Blog
{
    public int BlogId { get; set; }
    public string Name { get; set; }
}

class Program
{
    static void Main(string[] args)
    {
        using (var db = new BloggingContext())
        {
            // Create and save a new Blog
            Console.Write("Enter a name for a new Blog: ");
            var name = Console.ReadLine();
            var blog = new Blog { Name = name };
            db.Blogs.Add(blog);
            db.SaveChanges();

            // Display all Blogs from the database
            var query = from b in db.Blogs
                        orderby b.Name
                        select b;

            Console.WriteLine("All blogs in the database:");
            foreach (var item in query)
            {
                Console.WriteLine(item.Name);
            }
        }
    }
}
```

In this example, BloggingContext is the database context that manages the database connection and provides DbSet properties for querying and saving instances of the Blog class. The example demonstrates creating a new Blog instance, saving it to the database, and then querying and displaying all blogs. Entity Framework handles all the database interactions, allowing the developer to work at a higher level of abstraction.

Entity Framework significantly simplifies data access in .NET applications, making it an essential tool for rapid development while ensuring applications are maintainable and scalable.

### 19. What are extension methods and where would you use them?

**Answer:** Extension methods in C# allow developers to add new methods to existing types without modifying, deriving from, or recompiling the original types. They are static methods defined in a static class, but called as if they were instance methods on the extended type. Extension methods provide a flexible way to extend the functionality of a class or interface.

To use extension methods, the static class containing the extension method must be in scope, which usually requires a `using` directive for the namespace of the class.

Advantages of using extension methods include:
- Enhancing the functionality of third-party libraries or built-in .NET types without access to the original source code.
- Keeping code cleaner and more readable by encapsulating complex operations into methods.
- Facilitating a fluent interface style of coding, which can make code more expressive.

Here is a simple example demonstrating how to define and use an extension method:

```csharp
using System;

namespace ExtensionMethods
{
    public static class StringExtensions
    {
        // Extension method for the String class
        public static string ToPascalCase(this string input)
        {
            if (string.IsNullOrEmpty(input))
                return input;

            string[] words = input.Split(new char[] { ' ', '-' }, StringSplitOptions.RemoveEmptyEntries);
            for (int i = 0; i < words.Length; i++)
            {
                words[i] = char.ToUpper(words[i][0]) + words[i].Substring(1).ToLower();
            }
            return string.Join("", words);
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        string title = "the quick-brown fox";
        string pascalCaseTitle = title.ToPascalCase();
        Console.WriteLine(pascalCaseTitle); // Outputs: TheQuickBrownFox
    }
}
```

In this example, ToPascalCase is an extension method defined for the String class. It converts a given string to Pascal case format. To use this extension method, simply call it on a string instance, as shown in the Main method. This demonstrates how extension methods can add useful functionality to existing types in a clean and natural syntax.

Extension methods are a powerful feature for extending the capabilities of types, especially when direct modifications to the class are not possible or desirable.

### 20. How do you handle exceptions in a method that returns a Task?

**Answer:** In asynchronous programming with C#, when a method returns a `Task` or `Task<T>`, exceptions should be handled within the task to avoid unhandled exceptions that can crash the application. Exceptions thrown in a task are captured and placed on the returned task object. To handle these exceptions, you can use a try-catch block within the asynchronous method, or you can inspect the task after it has completed for any exceptions.

There are several approaches to handle exceptions in tasks:

1. **Inside the Asynchronous Method:**
   Use a try-catch block inside the async method to catch exceptions directly.

```csharp
public async Task PerformOperationAsync()
{
    try
    {
        // Async operation that may throw an exception
    }
    catch (Exception ex)
    {
        // Handle exception
    }
}
```

2. When Awaiting the Task:
Await the task inside a try-catch block to catch exceptions when the task is awaited.

```csharp

try
{
    await PerformOperationAsync();
}
catch (Exception ex)
{
    // Handle exception
}
```

3. Using Task.ContinueWith:
Use the ContinueWith method to attach a continuation task that can handle exceptions.

```csharp
PerformOperationAsync().ContinueWith(task =>
{
    if (task.Exception != null)
    {
        // Handle exception
        var exception = task.Exception.InnerException;
    }
}, TaskContinuationOptions.OnlyOnFaulted);
```

4. Using Task.WhenAny:
Useful for handling exceptions from multiple tasks.

```csharp

var task = PerformOperationAsync();
await Task.WhenAny(task); // Wait for task to complete

if (task.IsFaulted)
{
    // Handle exception
    var exception = task.Exception.InnerException;
}

```

Here is an example demonstrating handling exceptions for a method that returns a Task:

```csharp

public async Task<int> DivideAsync(int numerator, int denominator)
{
    return await Task.Run(() =>
    {
        if (denominator == 0)
            throw new DivideByZeroException("Denominator cannot be zero.");

        return numerator / denominator;
    });
}

public async Task ExecuteAsync()
{
    try
    {
        int result = await DivideAsync(10, 0);
        Console.WriteLine($"Result: {result}");
    }
    catch (DivideByZeroException ex)
    {
        Console.WriteLine($"Error: {ex.Message}");
    }
}
```

In this example, DivideAsync performs a division operation asynchronously and may throw a DivideByZeroException. The exception is handled in the ExecuteAsync method, demonstrating how to properly handle exceptions for tasks in asynchronous methods.

Handling exceptions in tasks is crucial for writing robust and error-resistant asynchronous C# applications, ensuring that your application can gracefully recover from errors encountered during asynchronous operations.

### 21. What is reflection in .NET and how would you use it?

**Answer:** Reflection in .NET is a powerful feature that allows runtime inspection of assemblies, types, and their members (such as methods, fields, properties, and events). It enables creating instances of types, invoking methods, and accessing fields and properties dynamically, without knowing the types at compile time. Reflection is used for various purposes, including building type browsers, dynamically invoking methods, and reading custom attributes.

Reflection can be particularly useful in scenarios such as:
- Dynamically loading and using assemblies.
- Implementing object browsers or debuggers.
- Creating instances of types for dependency injection frameworks.
- Accessing and manipulating metadata for assemblies and types.

Here's a simple example demonstrating how to use reflection to inspect and invoke methods of a class dynamically:

```csharp
using System;
using System.Reflection;

public class MyClass
{
    public void MethodToInvoke()
    {
        Console.WriteLine("Method Invoked.");
    }
}

class Program
{
    static void Main(string[] args)
    {
        // Obtaining the Type object for MyClass
        Type myClassType = typeof(MyClass);
        
        // Creating an instance of MyClass
        object myClassInstance = Activator.CreateInstance(myClassType);
        
        // Getting the MethodInfo object for MethodToInvoke
        MethodInfo methodInfo = myClassType.GetMethod("MethodToInvoke");
        
        // Invoking the method on the instance
        methodInfo.Invoke(myClassInstance, null);
    }
}
```

In this example, reflection is used to obtain the Type object for MyClass, create an instance of MyClass, and then retrieve and invoke the MethodToInvoke method. This demonstrates how reflection allows for dynamic type inspection and invocation, providing flexibility and power in how code interacts with objects.

Using reflection comes with a performance cost, so it should be used judiciously, especially in performance-critical paths of an application.

### 22. Can you explain the concept of middleware in ASP.NET Core?

**Answer:** Middleware in ASP.NET Core is software that's assembled into an application pipeline to handle requests and responses. Each component in the middleware pipeline is responsible for invoking the next component in the sequence or short-circuiting the chain if necessary. Middleware components can perform a variety of tasks, such as authentication, routing, session management, and logging.

Middleware enables you to customize the request pipeline in ways that are most suited to your application's needs. They are executed in the order they are added to the pipeline, allowing for precise control over how requests are processed and how responses are constructed.

Here's a simple example demonstrating how to create and use middleware in ASP.NET Core:

```csharp
public class CustomMiddleware
{
    private readonly RequestDelegate _next;

    public CustomMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        // Do something with the context before the next middleware
        Console.WriteLine("Before next middleware");

        await _next(context); // Call the next middleware in the pipeline

        // Do something with the context after the next middleware
        Console.WriteLine("After next middleware");
    }
}

// Extension method used to add the middleware to the application's request pipeline
public static class CustomMiddlewareExtensions
{
    public static IApplicationBuilder UseCustomMiddleware(this IApplicationBuilder builder)
    {
        return builder.UseMiddleware<CustomMiddleware>();
    }
}

public class Startup
{
    public void Configure(IApplicationBuilder app)
    {
        app.UseCustomMiddleware();
        // Other middleware registrations
    }
}
```

In this example, CustomMiddleware is defined with an InvokeAsync method that ASP.NET Core calls to process the HTTP request. The UseCustomMiddleware extension method adds the middleware to the application's request pipeline, and it's registered in the Configure method of the Startup class.

Middleware components in ASP.NET Core provide a powerful way to compose your application's request-handling pipeline, allowing for modular and reusable components that can encapsulate request-processing logic.

### 23. Describe the Dependency Injection (DI) pattern and how it's implemented in .NET Core.

**Answer:** Dependency Injection (DI) is a design pattern that facilitates loose coupling between software components by removing the direct dependencies among them. Instead of instantiating dependencies directly, components receive their dependencies from an external source (often an inversion of control container). DI makes your code more modular, easier to test, maintain, and extend.

.NET Core has built-in support for dependency injection, which allows services to be registered and resolved through an IoC (Inversion of Control) container. The container manages object creation and injects dependencies where required. This mechanism is central to ASP.NET Core applications, enabling features like middleware, controllers, views, and other services to be provided and managed by the framework.

The core concepts in .NET Core's DI system include:
- **Service registration:** Services are registered with the DI container, typically in the `Startup.ConfigureServices` method, specifying their lifetime (singleton, scoped, or transient).
- **Service resolution:** Services are resolved either through constructor injection, method call injection, or property injection, with constructor injection being the most common approach.

Here's a simple example demonstrating how DI is used in an ASP.NET Core application:

```csharp
public interface IGreetingService
{
    string Greet(string name);
}

public class GreetingService : IGreetingService
{
    public string Greet(string name)
    {
        return $"Hello, {name}!";
    }
}

public class HomeController : Controller
{
    private readonly IGreetingService _greetingService;

    public HomeController(IGreetingService greetingService)
    {
        _greetingService = greetingService;
    }

    public IActionResult Index()
    {
        var greeting = _greetingService.Greet("World");
        return Content(greeting);
    }
}

public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddControllersWithViews();
        services.AddTransient<IGreetingService, GreetingService>();
    }

    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        // Configure the request pipeline.
        app.UseRouting();

        app.UseEndpoints(endpoints =>
        {
            endpoints.MapDefaultControllerRoute();
        });
    }
}
```

In this example, IGreetingService is an interface defining a service contract, and GreetingService is its implementation. The service is registered with the DI container in the Startup.ConfigureServices method using services.AddTransient<IGreetingService, GreetingService>();. The HomeController receives an instance of IGreetingService through constructor injection, provided by the DI container. This demonstrates how DI facilitates loose coupling and enhances the testability and maintainability of the application.

Dependency Injection in .NET Core is a foundational feature that supports the development of decoupled and easily testable applications.

### 24. What is the purpose of the .NET Standard?

**Answer:** The .NET Standard is a formal specification of .NET APIs that are intended to be available on all .NET implementations. The goal of the .NET Standard is to establish greater uniformity in the .NET ecosystem. It enables developers to create libraries that are compatible across different .NET platforms, such as .NET Core, .NET Framework, Xamarin, and others, with a single codebase. This simplifies the development process and enhances code reuse across projects and platforms.

The .NET Standard is versioned, with each version building upon the previous one and adding more APIs. Higher versions of the .NET Standard support newer APIs but reduce the number of platforms that support that standard because older platforms may not implement the newer APIs.

Here's how the .NET Standard serves different roles in the .NET ecosystem:
- For library developers: It provides a base set of APIs that are guaranteed to be available on all .NET platforms, enabling the creation of portable libraries that can run on any .NET implementation.
- For application developers: It assures that any library targeting a version of the .NET Standard can be used in their application, regardless of the .NET platform it runs on.
- For .NET implementations: It establishes a baseline of APIs that must be implemented, ensuring compatibility and unification across different .NET platforms.

An example of targeting the .NET Standard in a class library project file (`csproj`):

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
  </PropertyGroup>

</Project>
```

In this example, the class library targets .NET Standard 2.0, meaning it can run on any .NET platform that supports .NET Standard 2.0 or higher. This includes .NET Core 2.0+, .NET Framework 4.6.1+, Xamarin, and others, making the library highly reusable across a wide range of applications and platforms.

The .NET Standard facilitates the development of portable libraries and helps unify the .NET ecosystem, making it easier for developers to share and reuse code across different .NET platforms.

### 25. Explain the differences between .NET Core, .NET Framework, and Xamarin.

**Answer:** .NET Core, .NET Framework, and Xamarin are all part of the .NET ecosystem, but they serve different purposes and are used in different types of projects. Understanding the differences between them can help you choose the right technology for your specific needs.

- **.NET Framework:**
  - The original .NET implementation, launched in 2002.
  - Primarily runs on Windows and is used for developing Windows desktop applications and ASP.NET web applications.
  - Provides a vast library of pre-built functionality, including Windows Forms, WPF (Windows Presentation Foundation) for desktop applications, and ASP.NET for web applications.
  - Moving forward, it will receive only critical security updates and bug fixes.

- **.NET Core:**
  - A cross-platform, open-source reimplementation of .NET that runs on Windows, macOS, and Linux.
  - Designed to be modular and lightweight, making it suitable for web applications, microservices, and cloud applications.
  - Supports development of console applications, ASP.NET Core web applications, and libraries.
  - With the release of .NET 5 and beyond, .NET Core has evolved into simply ".NET," unifying the .NET platform and serving as the future of the .NET ecosystem.

- **Xamarin:**
  - A .NET platform for building mobile applications that can run on iOS, Android, and Windows devices.
  - Allows developers to write mobile applications using C# and .NET libraries while providing native performance and look-and-feel on each platform.
  - Integrates with Visual Studio, providing a rich development environment.
  - Xamarin.Forms allows for the creation of UIs from a single, shared codebase, while Xamarin.iOS and Xamarin.Android provide access to platform-specific APIs.

Here's a simple comparison:

| Feature/Platform | .NET Framework | .NET Core           | Xamarin             |
|------------------|----------------|---------------------|---------------------|
| Platform         | Windows        | Cross-platform      | Mobile (iOS, Android, Windows) |
| Use Cases        | Desktop, Web   | Web, Microservices, Console | Mobile apps          |
| Development      | Visual Studio  | Visual Studio, VS Code, Others | Visual Studio, Visual Studio for Mac |
| Open Source      | No             | Yes                 | Yes                 |

.NET 5 and onwards (rebranded from .NET Core) aim to unify these platforms under a single .NET runtime and framework that can be used everywhere and that supports all types of application development.

### 26. How does garbage collection work in .NET and how can you optimize it?

**Answer:** Garbage Collection (GC) in .NET is an automatic memory management feature that helps in reclaiming the memory used by objects that are no longer accessible in the application. It eliminates the need for manual memory management, reducing the risks of memory leaks and other memory-related issues.

**How Garbage Collection Works:**
- **Mark:** The GC traverses the object graph to mark objects that are reachable, starting from root references. Reachable objects are considered "live".
- **Compact:** To reclaim the memory occupied by unreachable objects, the GC compacts the remaining objects, thus reducing the space used on the managed heap and making room for new objects.
- **Generations:** The GC uses a generational approach to manage memory collections, dividing the heap into three generations (0, 1, and 2) for more efficient garbage collection. Generation 0 is for short-lived objects, Generation 1 for medium-lived objects, and Generation 2 for long-lived objects. Collecting younger generations more frequently reduces the need to perform expensive collections on older generations.

**Optimizing Garbage Collection:**
1. **Minimize Allocations:** Be mindful of unnecessary allocations, especially in performance-critical paths. Reuse objects when possible, and consider using object pools for frequently created and destroyed objects.
2. **Understand Generations:** Knowing how generations work can help you write code that interacts more efficiently with the GC. For example, large objects are placed directly into Generation 2, so their allocation and deallocation can be expensive.
3. **Use Structs Judiciously:** Structs are value types and are allocated on the stack (when declared outside of a class). When used appropriately, they can reduce heap allocations. However, excessively large structs or inappropriate use can lead to performance issues.
4. **Implement IDisposable:** For classes that use unmanaged resources (like file handles or database connections), implement the `IDisposable` interface and dispose of those resources when they are no longer needed to free up resources promptly.
5. **Monitor and Analyze:** Use profiling tools to monitor your application's memory usage and GC behavior. Tools like Visual Studio Diagnostic Tools, dotMemory, and the GC API (`System.GC`) can provide insights into how your application interacts with the garbage collector.

Here's an example of implementing `IDisposable`:

```csharp
public class ResourceWrapper : IDisposable
{
    private bool disposed = false;

    // Assume _resource is an unmanaged resource.
    private IntPtr _resource;

    public ResourceWrapper()
    {
        _resource = // Allocate the resource
    }

    protected virtual void Dispose(bool disposing)
    {
        if (!disposed)
        {
            if (disposing)
            {
                // Dispose managed resources.
            }

            // Free unmanaged resources
            if (_resource != IntPtr.Zero)
            {
                // Free the resource
                _resource = IntPtr.Zero;
            }

            disposed = true;
        }
    }

    public void Dispose()
    {
        Dispose(true);
        GC.SuppressFinalize(this);
    }

    ~ResourceWrapper()
    {
        Dispose(false);
    }
}
```

By understanding and optimizing the .NET garbage collector, developers can improve their applications' performance and reliability.


### 27. What are attributes in C# and how can they be used?

**Answer:** Attributes in C# are a powerful way to add declarative information to your code. They are used to add metadata, such as compiler instructions, annotations, or custom information, to program elements (classes, methods, properties, etc.). Attributes can influence the behavior of certain components at runtime or compile time, and they can be queried through reflection.

**Common Uses of Attributes:**
- Marking methods as test methods in a unit testing framework (e.g., `[TestMethod]` in MSTest).
- Specifying serialization rules (e.g., `[Serializable]`, `[DataMember]`).
- Controlling binding and model validation in ASP.NET Core (e.g., `[Required]`, `[Bind]`).
- Defining aspects of web service behaviors (e.g., `[WebMethod]`).
- Custom attributes for domain-specific purposes.

**Example of Using an Attribute:**

A common use case is data validation in ASP.NET Core models. The `[Required]` attribute indicates that a property must have a value; if a model is passed to a controller method without this property set, model validation fails.

```csharp
using System.ComponentModel.DataAnnotations;

public class Person
{
    [Required]
    public string Name { get; set; }

    [Range(1, 120)]
    public int Age { get; set; }
}
```

**Creating Custom Attributes:**

You can also define custom attributes for specific needs. Here's a simple example:

```csharp

[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, AllowMultiple = false)]
public class MyCustomAttribute : Attribute
{
    public string Description { get; set; }

    public MyCustomAttribute(string description)
    {
        Description = description;
    }
}

[MyCustomAttribute("This is a class description.")]
public class MyClass
{
    [MyCustomAttribute("This is a method description.")]
    public void MyMethod() { }
}
```

In this example, MyCustomAttribute is defined with a property Description. It can be attached to classes or methods, providing custom descriptive metadata. The AttributeUsage attribute specifies where this attribute can be applied (Class or Method) and whether it can be used multiple times on the same element (AllowMultiple).

Attributes extend the capabilities of C# by allowing you to define additional information about the behavior and structure of your code in a declarative manner. They are a key part of many .NET frameworks and libraries, enabling various runtime behaviors and compile-time checks.

### 28. Can you describe the process of code compilation in .NET?

**Answer:** The process of code compilation in .NET involves converting high-level code (such as C#) into a platform-independent Intermediate Language (IL) and then into platform-specific machine code. This process is facilitated by the .NET Compiler Platform ("Roslyn" for C# and Visual Basic) and the Common Language Runtime (CLR). Here's an overview of the steps involved:

1. **Source Code to Intermediate Language (IL):**
   - When you compile a .NET application, the .NET compiler for your language (e.g., csc.exe for C#) compiles the source code into Intermediate Language (IL). IL is a CPU-independent set of instructions that can be efficiently converted into native machine code.
   - Along with IL, metadata is generated, which includes information about the types, members, references, and other data that the IL code uses.

2. **IL to Native Code:**
   - At runtime, the .NET application is executed by the CLR. The CLR's Just-In-Time (JIT) compiler converts the IL code into native machine code specific to the architecture of the target machine.
   - This conversion happens on a need-to-run basis; that is, each method's IL is converted to native code the first time the method is called. The native code is then cached, so subsequent calls to the same method do not require re-compilation.

3. **Execution:**
   - The native code is executed directly by the hardware of the target machine, leading to the execution of the .NET application.

**Aspects of .NET Compilation:**

- **Assembly:** The compiled code and resources are packed into assemblies (`.dll` or `.exe` files), which are the units of deployment and versioning in .NET. Assemblies contain the IL code and metadata.
- **Metadata:** Metadata describes the assembly itself and the types defined within the assembly, including their methods and properties. This information is used by the CLR during execution and supports features like reflection.
- **Strong Naming and GAC:** Assemblies can be strong-named to ensure their uniqueness and integrity. Strong-named assemblies can be placed in the Global Assembly Cache (GAC) for shared use by multiple applications.

**Optimizations and NGEN:**

- The JIT compiler applies various optimizations while converting IL to native code to improve runtime performance. Additionally, developers can use the Native Image Generator (NGEN) to pre-compile assemblies into native images at install time, reducing JIT compilation time at runtime but at the cost of losing some JIT optimizations specific to the end-user's machine.

```csharp
// Example C# code
public class Program
{
    public static void Main(string[] args)
    {
        Console.WriteLine("Hello, World!");
    }
}
```

This simple program is compiled to IL when built and then JIT-compiled to native code by the CLR when executed.
Understanding the compilation process in .NET is crucial for grasping how .NET applications are built, deployed, and executed across different environments and platforms.

### 29. What is the Global Assembly Cache (GAC) and when should it be used?

**Answer:** The Global Assembly Cache (GAC) is a machine-wide code cache for the Common Language Runtime (CLR) in the .NET Framework. It stores assemblies specifically designated to be shared by several applications on the computer. The GAC is used to store shared .NET assemblies that have strong names (which are unique identifiers consisting of a name, version number, culture information, and a public key token).

**Key Points about the GAC:**

- **Sharing Assemblies:** The GAC allows multiple applications to share the same library, reducing memory usage and ensuring consistency across applications that use common components.
- **Strong Naming:** Only assemblies with strong names (signed with a public/private key pair) can be added to the GAC. Strong naming guarantees the uniqueness of the assembly's identity, allowing side-by-side hosting of different versions.
- **Versioning:** The GAC supports side-by-side execution of different versions of the same assembly. This enables applications to specify and use the version of an assembly they were built with, even if newer versions are installed on the system.

**When to Use the GAC:**

- **Shared Libraries:** Use the GAC for assemblies that need to be shared by multiple applications on the same machine. Common libraries or frameworks that are stable and versioned are good candidates.
- **Side-by-Side Hosting:** When different versions of the same assembly need to be used by different applications on the same system, deploying these assemblies to the GAC can manage versioning complexities.
- **Security:** Assemblies in the GAC are generally more secure, as only users with administrative privileges can add or remove assemblies. This control can prevent malicious code from being inadvertently added to the cache.

**Example of Adding an Assembly to the GAC:**

To add an assembly to the GAC, you can use the `gacutil` tool provided with the .NET Framework SDK:

```bash
gacutil -i MyAssembly.dll
```

This command installs MyAssembly.dll into the GAC.

Note: With the introduction of .NET Core and its focus on application-local deployment models, the GAC is less emphasized and is specific to the .NET Framework. .NET Core and .NET 5+ applications typically rely on package management systems like NuGet to handle dependencies and do not use the GAC.

The GAC plays a critical role in assembly sharing and versioning in the .NET Framework, facilitating the management of common libraries across applications on a single machine.

## 30. How would you secure a web application in ASP.NET Core?
Securing an ASP.NET Core web application involves multiple strategies, including authentication, authorization, data protection, and HTTPS enforcement.

### Example: Enforcing HTTPS in ASP.NET Core
```csharp
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    app.UseHttpsRedirection(); // Redirect HTTP requests to HTTPS
    app.UseAuthentication();   // Enable authentication middleware
    app.UseAuthorization();    // Enable authorization middleware
}
```
---

## 31. What is MVC (Model-View-Controller)?
MVC is a software design pattern that separates an application into three components:

- **Model**: Represents the data and business logic.

- **View**: Handles the presentation layer.

- **Controller**: Manages user input and updates the model.

### Example: A Simple MVC Controller in ASP.NET Core
```csharp
public class HomeController : Controller
{
    public IActionResult Index()
    {
        return View();
    }
}
```
---

## 32. Can you explain the difference between Razor Pages and MVC in ASP.NET Core?
- **MVC** uses a Controller to handle requests, while **Razor Pages** has built-in page handlers (`OnGet`, `OnPost`).
- Razor Pages is more suitable for simple, page-focused applications, whereas MVC is better for larger applications.

### Example: Razor Page Handler
```csharp
public class IndexModel : PageModel
{
    public void OnGet()
    {
        // Handle GET request
    }
}
```
---

## 33. How do you perform validations in ASP.NET Core?
ASP.NET Core provides validation using **Data Annotations** and **Fluent Validation**.

### Example: Using Data Annotations
```csharp
public class UserModel
{
    [Required]
    [EmailAddress]
    public string Email { get; set; }

    [Required]
    [MinLength(6)]
    public string Password { get; set; }
}
```
---

## 34. Describe SignalR and its use cases.
SignalR is a real-time communication library in ASP.NET Core that enables WebSockets for interactive web applications.

### Example: SignalR Hub
```csharp
public class ChatHub : Hub
{
    public async Task SendMessage(string user, string message)
    {
        await Clients.All.SendAsync("ReceiveMessage", user, message);
    }
}
```
---

## 35. What are the benefits of using Blazor over traditional web technologies?
Blazor allows building web applications using **C# and .NET** instead of JavaScript.

### Example: Blazor Component
```csharp
@code {
    string message = "Hello, Blazor!";
}
<p>@message</p>
```
---

## 36. How do you implement Web API versioning in ASP.NET Core?
API versioning ensures backward compatibility for REST APIs.

### Example: Using API Versioning Middleware
```csharp
services.AddApiVersioning(o =>
{
    o.ReportApiVersions = true;
    o.AssumeDefaultVersionWhenUnspecified = true;
    o.DefaultApiVersion = new ApiVersion(1, 0);
});
```
---

## 37. Explain the role of `IApplicationBuilder` in ASP.NET Core.
`IApplicationBuilder` is used in `Startup.Configure()` to define the middleware pipeline.

### Example:
```csharp
public void Configure(IApplicationBuilder app)
{
    app.UseRouting();
    app.UseAuthorization();
    app.UseEndpoints(endpoints => endpoints.MapControllers());
}
```
---

## 38. What are Areas in ASP.NET Core and how do you use them?
Areas help organize large MVC applications by grouping controllers, views, and models.

### Example: Defining an Area
```csharp
[Area("Admin")]
public class DashboardController : Controller
{
    public IActionResult Index() => View();
}
```
---

## 39. How do you manage sessions in ASP.NET Core applications?
ASP.NET Core provides session state management using `ISession`.

### Example:
```csharp
services.AddSession();

app.UseSession();

HttpContext.Session.SetString("User", "Admin");
string user = HttpContext.Session.GetString("User");
```
---

## 40. Describe how to implement caching in ASP.NET Core.
ASP.NET Core supports memory caching and distributed caching.

### Example: In-Memory Caching
```csharp
services.AddMemoryCache();

public class MyService
{
    private readonly IMemoryCache _cache;
    public MyService(IMemoryCache cache) { _cache = cache; }

    public string GetData()
    {
        return _cache.GetOrCreate("cachedData", entry => "Hello, Cache!"); 
    }
}
```
---

## 41. What is Unit Testing in .NET?
Unit testing is the practice of testing individual components of an application in isolation.

### Example: NUnit Unit Test
```csharp
[Test]
public void TestSum()
{
    int result = Calculator.Sum(2, 3);
    Assert.AreEqual(5, result);
}
```
---

## 42. How do you mock dependencies in unit tests using .NET?
Mocking is used to simulate dependencies in unit tests using **Moq**.

### Example:
```csharp
var mockRepo = new Mock<IRepository>();
mockRepo.Setup(repo => repo.GetData()).Returns("Mock Data");
```
---

## 43. Can you explain SOLID principles?
**SOLID** is a set of five principles for writing maintainable code:

1. **S**ingle Responsibility Principle

2. **O**pen/Closed Principle

3. **L**iskov Substitution Principle

4. **I**nterface Segregation Principle

5. **D**ependency Inversion Principle
---

## 44. What is Continuous Integration/Continuous Deployment (CI/CD)?
CI/CD automates code integration, testing, and deployment.

### Example: GitHub Actions for CI/CD
```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v2
      - name: Build and Test
        run: dotnet test
```
## 45. How do you ensure your C# code is secure?
Writing secure C# code requires following best practices to prevent vulnerabilities such as SQL injection, cross-site scripting (XSS), and unauthorized access.

### Key Security Measures:
- **Use parameterized queries** to prevent SQL injection.
- **Hash and salt passwords** using `BCrypt` or `PBKDF2`.
- **Enable HTTPS** to encrypt communication.
- **Validate user input** to prevent injection attacks.
- **Use dependency injection (DI)** to avoid hardcoded secrets.

### Example: Preventing SQL Injection
```csharp
using System.Data.SqlClient;

public void GetUser(int userId)
{
    using (SqlConnection conn = new SqlConnection("connectionString"))
    {
        string query = "SELECT * FROM Users WHERE Id = @userId";
        using (SqlCommand cmd = new SqlCommand(query, conn))
        {
            cmd.Parameters.AddWithValue("@userId", userId);
            conn.Open();
            var reader = cmd.ExecuteReader();
            while (reader.Read())
            {
                Console.WriteLine(reader["Name"]);
            }
        }
    }
}
```
Here, **parameterized queries** prevent SQL injection.

---

## 46. What are some common performance issues in .NET applications and how do you address them?
Performance issues in .NET applications often arise due to inefficient memory usage, slow database queries, or excessive allocations.

### Common Performance Issues and Fixes:
- **Memory Leaks** → Use `IDisposable` and `using` statements.
- **Slow Queries** → Optimize SQL queries and indexing.
- **Excessive Object Allocations** → Use object pooling and struct types.

### Example: Using Caching to Improve Performance
```csharp
public class DataService
{
    private readonly IMemoryCache _cache;
    public DataService(IMemoryCache cache)
    {
        _cache = cache;
    }

    public string GetData()
    {
        return _cache.GetOrCreate("cachedData", entry =>
        {
            entry.AbsoluteExpirationRelativeToNow = TimeSpan.FromMinutes(5);
            return "Cached Data";
        });
    }
}
```
Using **in-memory caching** reduces expensive database calls.

---

## 47. Describe the Repository pattern and its benefits.
The **Repository Pattern** abstracts the data layer, providing a clean way to manage database operations.

### Benefits:
- **Separation of concerns** → Keeps data access logic separate.
- **Easier testing** → Allows mocking of database operations.
- **Code reusability** → Centralizes data access logic.

### Example: Repository Pattern in ASP.NET Core
```csharp
public interface IUserRepository
{
    IEnumerable<User> GetAllUsers();
    User GetUserById(int id);
}

public class UserRepository : IUserRepository
{
    private readonly AppDbContext _context;
    
    public UserRepository(AppDbContext context)
    {
        _context = context;
    }
    
    public IEnumerable<User> GetAllUsers() => _context.Users.ToList();

    public User GetUserById(int id) => _context.Users.Find(id);
}
```
Here, the `UserRepository` encapsulates database operations.

---

## 48. How do you handle database migrations in Entity Framework?
Migrations in Entity Framework allow changes to the database schema while preserving existing data.

### Steps to Apply Migrations:
1. **Add a new migration:**
   ```shell
   dotnet ef migrations add InitialCreate
   ```
2. **Apply the migration to the database:**
   ```shell
   dotnet ef database update
   ```

### Example: Defining a Model with Migrations
```csharp
public class User
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Email { get; set; }
}
```
Adding a migration for this model will create a corresponding database table.

---

## 49. What tools do you use for debugging and profiling .NET applications?
Effective debugging and profiling tools help identify performance bottlenecks and runtime errors.

### Popular Tools:
- **Visual Studio Debugger** → Step-through debugging.
- **dotTrace** → Identifies CPU-intensive operations.
- **BenchmarkDotNet** → Measures code performance.
- **dotMemory** → Finds memory leaks.

### Example: Using BenchmarkDotNet to Measure Performance
```csharp
[MemoryDiagnoser]
public class PerformanceTests
{
    [Benchmark]
    public void TestMethod()
    {
        var list = new List<int>();
        for (int i = 0; i < 1000; i++)
        {
            list.Add(i);
        }
    }
}
```
Here, **BenchmarkDotNet** measures memory usage and execution time.

---

## 50. How do you stay updated with the latest .NET technologies and practices?
Staying current with .NET advancements ensures that you use the best tools and frameworks.

### Recommended Ways to Stay Updated:
- **Follow Microsoft's .NET Blog** → [https://devblogs.microsoft.com/dotnet/](https://devblogs.microsoft.com/dotnet/)
- **Attend Conferences/Webinars** → .NET Conf, Microsoft Build
- **Join Online Communities** → GitHub, Stack Overflow, Twitter

---

## 51. **What is the difference between INNER JOIN, LEFT JOIN, RIGHT JOIN, and FULL JOIN?**

**Answer:**  
These SQL join types determine how rows from two tables are combined based on a related column.

- **INNER JOIN**: Returns only rows where there is a match in both tables.
- **LEFT JOIN**: Returns all rows from the left table and matching rows from the right. NULLs if no match.
- **RIGHT JOIN**: Returns all rows from the right table and matching rows from the left. NULLs if no match.
- **FULL JOIN**: Returns all rows when there is a match in either table. NULLs where no match exists.

---

### Example Tables

**Customers**

| Id | Name     |
|----|----------|
| 1  | Alice    |
| 2  | Bob      |
| 3  | Charlie  |

**Orders**

| Id | CustomerId | Product   |
|----|------------|-----------|
| 1  | 1          | Keyboard  |
| 2  | 1          | Mouse     |
| 3  | 2          | Monitor   |
| 4  | 4          | Webcam    |

---

### INNER JOIN

```sql
SELECT Customers.Name, Orders.Product
FROM Customers
INNER JOIN Orders ON Customers.Id = Orders.CustomerId;
```

**Result:**

| Name  | Product  |
|-------|----------|
| Alice | Keyboard |
| Alice | Mouse    |
| Bob   | Monitor  |

---

### LEFT JOIN

```sql
SELECT Customers.Name, Orders.Product
FROM Customers
LEFT JOIN Orders ON Customers.Id = Orders.CustomerId;
```

**Result:**

| Name    | Product  |
|---------|----------|
| Alice   | Keyboard |
| Alice   | Mouse    |
| Bob     | Monitor  |
| Charlie | NULL     |

---

### RIGHT JOIN

```sql
SELECT Customers.Name, Orders.Product
FROM Customers
RIGHT JOIN Orders ON Customers.Id = Orders.CustomerId;
```

**Result:**

| Name  | Product  |
|-------|----------|
| Alice | Keyboard |
| Alice | Mouse    |
| Bob   | Monitor  |
| NULL  | Webcam   |

---

### FULL JOIN

```sql
SELECT Customers.Name, Orders.Product
FROM Customers
FULL OUTER JOIN Orders ON Customers.Id = Orders.CustomerId;
```

**Result:**

| Name    | Product  |
|---------|----------|
| Alice   | Keyboard |
| Alice   | Mouse    |
| Bob     | Monitor  |
| Charlie | NULL     |
| NULL    | Webcam   |

--- 

## 52. **What is a primary key and how does it differ from a unique key?**

**Answer:**  
A **primary key** is a column or combination of columns that uniquely identifies each row in a table. It ensures that:

- Values are **unique** across rows.
- Values are **not NULL**.
- Each table can only have **one primary key**.

A **unique key** also ensures uniqueness of values, but:

- It **can allow NULLs** (depending on the database system).
- A table can have **multiple unique keys**.
- It is typically used to enforce business rules, like ensuring email or username is unique.

---

### Example: Primary Key vs Unique Key

```sql
CREATE TABLE Employees (
    EmployeeId INT PRIMARY KEY,          -- Primary key
    Email NVARCHAR(100) UNIQUE,          -- Unique key
    SSN CHAR(9) UNIQUE,                  -- Another unique key
    FullName NVARCHAR(100)
);
```

**Explanation:**
- `EmployeeId` is the primary key — must be unique and cannot be NULL.
- `Email` and `SSN` must also be unique, but can be NULL (depends on the RDBMS).
- You can have only one primary key, but multiple unique keys.

---

### Comparison Table

| Feature              | Primary Key        | Unique Key         |
|----------------------|--------------------|---------------------|
| Uniqueness           | ✅ Ensured          | ✅ Ensured           |
| NULLs allowed        | ❌ Not allowed      | ✅ Allowed (usually) |
| Number per table     | 1 only              | Multiple allowed     |
| Default index type   | Clustered (default) | Non-clustered (usually) |
| Used for             | Row identity        | Business rules       |

---

## 53. **What are foreign keys and how do they enforce referential integrity?**

**Answer:**  
A **foreign key** is a constraint used to link two tables together. It enforces **referential integrity** by ensuring that the value in one table (child) corresponds to a valid value in another table (parent).

- It prevents inserting invalid references.
- It restricts deleting parent rows that are referenced by child rows (unless cascading is enabled).

---

### Example

```sql
-- Parent table
CREATE TABLE Customers (
    Id INT PRIMARY KEY,
    Name NVARCHAR(100)
);

-- Child table with a foreign key
CREATE TABLE Orders (
    Id INT PRIMARY KEY,
    CustomerId INT,
    Product NVARCHAR(100),
    FOREIGN KEY (CustomerId) REFERENCES Customers(Id)
);
```

This ensures that every `CustomerId` in `Orders` must exist in `Customers`.

---

### Benefits

- Maintains consistency between related tables.
- Helps avoid orphaned records.
- Supports cascading operations (`ON DELETE`, `ON UPDATE`).

---

## 54. **Explain normalization and list the different normal forms.**

**Answer:**  
**Normalization** is the process of organizing data in a database to reduce **redundancy** and improve **data integrity**.

Each level of normalization is called a **normal form** (NF):

- **1NF (First Normal Form)**  
  - Ensures each column contains atomic (indivisible) values.  
  - No repeating groups or arrays in rows.

- **2NF (Second Normal Form)**  
  - Must be in 1NF.  
  - All non-key attributes are fully functionally dependent on the **entire** primary key (eliminates partial dependency).

- **3NF (Third Normal Form)**  
  - Must be in 2NF.  
  - No transitive dependency (non-key attributes depend only on the key, not on other non-key attributes).

---

### Example

#### Unnormalized Table (Repeating groups):

| OrderId | Customer | Products         |
|---------|----------|------------------|
| 1       | Alice    | Mouse, Keyboard  |

#### 1NF (Atomic values):

| OrderId | Customer | Product   |
|--------|----------|-----------|
| 1      | Alice    | Mouse     |
| 1      | Alice    | Keyboard  |

#### 2NF (Split into Orders and Customers):

**Customers**

| CustomerId | Name   |
|------------|--------|
| 1          | Alice  |

**Orders**

| OrderId | CustomerId | Product   |
|---------|------------|-----------|
| 1       | 1          | Mouse     |
| 2       | 1          | Keyboard  |

---

### Why Normalize?

- Eliminates data duplication.
- Reduces anomalies in insert/update/delete.
- Improves data integrity and maintainability.

---

## 55. **What is a clustered index vs a non-clustered index?**

**Answer:**  
Indexes improve data retrieval speed in SQL. There are two main types:

- **Clustered Index**
  - Determines the **physical order** of rows in the table.
  - A table can have **only one** clustered index.
  - Data is **stored in the same order** as the clustered index.
  - Typically created on the **primary key**.

- **Non-Clustered Index**
  - Contains a pointer to the actual data row.
  - A table can have **multiple** non-clustered indexes.
  - Does **not affect** the physical order of data.

---

### Example

```sql
-- Clustered index (usually created by default on primary key)
CREATE TABLE Employees (
    Id INT PRIMARY KEY,       -- clustered index
    Name NVARCHAR(100),
    Email NVARCHAR(100)
);

-- Non-clustered index
CREATE NONCLUSTERED INDEX IX_Employees_Email
ON Employees (Email);
```

---

### Comparison Table

| Feature             | Clustered Index       | Non-Clustered Index     |
|---------------------|------------------------|--------------------------|
| Physical sort order | Yes                    | No                       |
| Number per table    | One                    | Many                     |
| Storage             | Table data itself      | Separate index structure |
| Access speed        | Faster for range queries | Good for lookups         |

---

## 56. **What are transactions in SQL and what are ACID properties?**

**Answer:**  
A **transaction** is a sequence of operations performed as a **single logical unit of work**. Transactions follow the **ACID** properties to ensure data integrity.

---

### ACID Properties

- **Atomicity**: All operations succeed or none at all.
- **Consistency**: Brings the database from one valid state to another.
- **Isolation**: Transactions run independently of each other.
- **Durability**: Once committed, the results are permanent, even in the case of a crash.

---

### Example

```sql
BEGIN TRANSACTION;

UPDATE Accounts SET Balance = Balance - 100 WHERE Id = 1;
UPDATE Accounts SET Balance = Balance + 100 WHERE Id = 2;

-- Commit changes only if both succeed
COMMIT;

-- If something goes wrong
-- ROLLBACK;
```

---

### Why Use Transactions?

- Prevents partial updates.
- Ensures consistency during concurrent operations.
- Essential in financial and critical data operations.

---

## 57. **What is the difference between DELETE, TRUNCATE, and DROP?**

**Answer:**  
These SQL commands are used to remove data, but they differ in scope and behavior:

- **DELETE**
  - Removes rows **one at a time** based on a `WHERE` clause.
  - **Can be rolled back** if inside a transaction.
  - **Fires triggers** (if defined).
  - **Slower** for large datasets.

- **TRUNCATE**
  - Removes **all rows** from a table instantly.
  - Cannot use `WHERE`.
  - **Minimal logging**, so it's much **faster**.
  - Cannot be rolled back in some RDBMS (e.g., MySQL); in others (like SQL Server), it can be if within a transaction.
  - **Does not fire** triggers.

- **DROP**
  - Completely **removes the table or object** from the database.
  - Deletes the structure, data, indexes, constraints — everything.
  - **Cannot be rolled back**.

---

### Example

```sql
-- DELETE specific records
DELETE FROM Employees WHERE Department = 'Sales';

-- TRUNCATE all records
TRUNCATE TABLE Employees;

-- DROP the table entirely
DROP TABLE Employees;
```

---

### Comparison Table

| Feature          | DELETE             | TRUNCATE           | DROP              |
|------------------|--------------------|--------------------|-------------------|
| Removes data     | ✅ Row-by-row       | ✅ All at once      | ✅ Entire table    |
| WHERE supported  | ✅ Yes              | ❌ No              | ❌ No              |
| Rollback support | ✅ Yes              | ⚠️ Depends on RDBMS | ❌ No              |
| Fires triggers   | ✅ Yes              | ❌ No              | ❌ No              |
| Affects structure| ❌ No               | ❌ No               | ✅ Yes             |

---

## 58. **What are window functions in SQL and when would you use them?**

**Answer:**  
**Window functions** perform calculations across a set of rows that are **related to the current row**, without collapsing rows like `GROUP BY`.

They are useful for:
- Ranking
- Running totals
- Moving averages
- Percentiles

---

### Common Window Functions

- `ROW_NUMBER()`
- `RANK()`
- `DENSE_RANK()`
- `SUM() OVER()`
- `AVG() OVER()`
- `LAG() / LEAD()`

---

### Example

```sql
SELECT
    EmployeeId,
    Department,
    Salary,
    RANK() OVER (PARTITION BY Department ORDER BY Salary DESC) AS SalaryRank
FROM Employees;
```

**Explanation:**
- Ranks employees by salary **within each department**.
- Does not group rows — every row is retained.

---

### Use Cases

- Paginating results (`ROW_NUMBER()` with `OFFSET`)
- Top-N queries per category
- Comparing a row to the previous or next row (`LAG`, `LEAD`)
- Cumulative totals

--- 

## 59. **How does a Common Table Expression (CTE) work and how is it different from a subquery?**

**Answer:**  
A **Common Table Expression (CTE)** is a named temporary result set defined using the `WITH` keyword. It improves readability and can reference itself (recursive CTEs).

---

### Syntax

```sql
WITH CTE_Name AS (
    SELECT Column1, Column2
    FROM SomeTable
    WHERE Condition
)
SELECT * FROM CTE_Name;
```

---

### Benefits of CTEs

- Improves query **readability**.
- Can be **recursive**.
- Makes complex logic easier to structure.
- Reusable within the same query (unlike subqueries which are repeated).

---

### Subquery vs CTE

| Feature            | Subquery              | CTE                         |
|--------------------|-----------------------|-----------------------------|
| Readability        | Can get messy         | Cleaner and more readable  |
| Reuse              | Cannot be reused      | Can be referenced multiple times |
| Recursion support  | ❌ No                 | ✅ Yes                     |
| Performance        | Similar in most cases | Similar in most cases       |

---

### Example – CTE vs Subquery

**CTE version:**

```sql
WITH SalesAboveAvg AS (
    SELECT * FROM Sales
    WHERE Amount > (SELECT AVG(Amount) FROM Sales)
)
SELECT * FROM SalesAboveAvg;
```

**Subquery version:**

```sql
SELECT * FROM Sales
WHERE Amount > (SELECT AVG(Amount) FROM Sales);
```

---

## 60. **What are the advantages and disadvantages of using stored procedures?**

**Answer:**  
**Stored procedures** are precompiled SQL statements stored in the database, often used to encapsulate business logic.

---

### Advantages

- **Performance**: Precompiled execution = faster for repeated calls.
- **Security**: Can restrict access to underlying tables.
- **Reusability**: Encapsulate logic in one place.
- **Maintainability**: Logic changes don't require application recompilation.

---

### Disadvantages

- **Complexity**: Business logic may be scattered between code and DB.
- **Debugging**: Harder to debug than application logic.
- **Portability**: Tied to a specific RDBMS (T-SQL vs PL/pgSQL etc.).
- **Versioning**: Not as easy to track in source control.

---

### Example

```sql
CREATE PROCEDURE GetTopSellingProducts
    @MinQuantity INT
AS
BEGIN
    SELECT ProductName, SUM(Quantity) AS TotalSold
    FROM OrderDetails
    GROUP BY ProductName
    HAVING SUM(Quantity) > @MinQuantity;
END;
```

```sql
-- Execute the procedure
EXEC GetTopSellingProducts @MinQuantity = 50;
```

---

## 61. **How can you detect and prevent SQL injection?**

**Answer:**  
**SQL injection** is a security vulnerability where attackers inject malicious SQL code through user input. To detect and prevent it:

---

### Prevention Techniques

- ✅ **Use parameterized queries / prepared statements**  
- ✅ **Use ORM frameworks** (e.g., Entity Framework) which handle parameters internally  
- ✅ **Validate and sanitize user input**  
- ✅ **Least privilege principle** — avoid excessive DB permissions  
- ✅ **Avoid dynamic SQL** unless necessary, and always parameterize it  
- ✅ **Use stored procedures** with parameters

---

### Example — Unsafe (vulnerable to SQL injection):

```csharp
// DANGEROUS! Never concatenate user input into SQL
var query = "SELECT * FROM Users WHERE Username = '" + username + "'";
```

---

### Example — Safe (parameterized):

```csharp
var query = "SELECT * FROM Users WHERE Username = @username";
var command = new SqlCommand(query, connection);
command.Parameters.AddWithValue("@username", username);
```

---

### Example — EF Core Safe Interpolation:

```csharp
var user = await context.Users
    .FromSqlInterpolated($"SELECT * FROM Users WHERE Username = {username}")
    .FirstOrDefaultAsync();
```

---

## 62. **What is the difference between EXISTS and IN operators in SQL?**

**Answer:**  
Both `EXISTS` and `IN` are used to filter query results based on another set of results, but they work differently:

---

### `IN` operator:

- Compares a value to a **list of values** returned by a subquery.
- Subquery is evaluated and loaded into memory first.
- Suitable when working with **small to medium** result sets.

---

### `EXISTS` operator:

- Checks for **existence of rows** returned by a subquery.
- Returns **true immediately** when a match is found.
- Often faster with **large or correlated** datasets.

---

### Example — IN

```sql
SELECT Name
FROM Customers
WHERE Id IN (SELECT CustomerId FROM Orders);
```

---

### Example — EXISTS

```sql
SELECT Name
FROM Customers c
WHERE EXISTS (
    SELECT 1 FROM Orders o WHERE o.CustomerId = c.Id
);
```

### Performance Consideration

| Criteria             | IN                         | EXISTS                         |
|----------------------|----------------------------|---------------------------------|
| Use case             | Value comparison           | Existence check                |
| Subquery execution   | All results loaded         | Stops at first match           |
| Works with NULLs     | Can be problematic         | ✅ Handles NULLs gracefully     |
| Ideal for            | Small datasets             | Large datasets / correlated queries |

---

## 63. **How does indexing work and how can you identify slow queries?**

**Answer:**  
An **index** is a database structure that improves the speed of data retrieval operations on a table at the cost of additional storage and slower write operations (INSERT, UPDATE, DELETE).

---

### How Indexing Works

- Works like a **lookup table** for faster data access.
- **B-tree structure** is most common.
- Indexes store a sorted list of column values and pointers to their corresponding rows.

---

### Types of Indexes

- **Clustered Index**: Sorts the physical data in the table (only one per table).
- **Non-Clustered Index**: Stores index separately from table data (many allowed).
- **Composite Index**: Index on multiple columns.
- **Covering Index**: Contains all columns needed by a query.

---

### Identifying Slow Queries

- Use **query execution plans** to analyze performance.
- Look for **table scans** or **missing index warnings**.
- Tools to use:
  - SQL Server: **Execution Plan**, **SQL Profiler**
  - PostgreSQL: **EXPLAIN ANALYZE**
  - MySQL: **EXPLAIN**

---

### Example — Creating Index

```sql
-- Create index on LastName column
CREATE INDEX IX_Employees_LastName ON Employees(LastName);
```

---

## 64. **What is the use of the `EXPLAIN` or `QUERY PLAN` statement?**

**Answer:**  
`EXPLAIN` (or `EXPLAIN ANALYZE`) shows the **query execution plan**, which details how the database engine will execute a SQL query.

---

### What It Helps With

- Reveals **which indexes are used**
- Shows **join algorithms** (nested loop, hash join, etc.)
- Identifies **bottlenecks** like full table scans
- Estimates **row counts and costs**

---

### Syntax Examples

**PostgreSQL:**

```sql
EXPLAIN ANALYZE
SELECT * FROM Orders WHERE CustomerId = 5;
```

**SQL Server:**

```sql
-- Enable actual execution plan
-- Ctrl + M in SSMS before running query
SELECT * FROM Orders WHERE CustomerId = 5;
```

**MySQL:**

```sql
EXPLAIN
SELECT * FROM Orders WHERE CustomerId = 5;
```

---

### Example Output Highlights

| Field        | Meaning                            |
|--------------|-------------------------------------|
| Seq Scan     | Sequential (table) scan occurred   |
| Index Scan   | Index was used                     |
| Rows         | Estimated number of rows processed |
| Cost         | Estimated time/memory cost         |

---

### Why It's Useful

- Helps you **optimize queries** and index usage.
- Essential for troubleshooting **performance issues**.

---

## 65. **What are aggregate functions and how are GROUP BY and HAVING used?**

**Answer:**  
**Aggregate functions** perform calculations on a set of values and return a single value. Common aggregate functions include:

- `COUNT()` – total number of rows
- `SUM()` – total value
- `AVG()` – average value
- `MIN()` – minimum value
- `MAX()` – maximum value

---

### GROUP BY

- Groups rows that have the same values in specified columns into summary rows.
- Used with aggregate functions to produce grouped results.

### HAVING

- Filters the results **after** grouping has been applied.
- Similar to `WHERE`, but works with aggregate values.

---

### Example

```sql
SELECT Department, COUNT(*) AS EmployeeCount
FROM Employees
GROUP BY Department
HAVING COUNT(*) > 5;
```

**Explanation:**
- Groups employees by department.
- Only shows departments with more than 5 employees.

---

### GROUP BY vs HAVING vs WHERE

| Clause  | Filters Before/After Aggregation | Can Use Aggregates? |
|---------|-------------------------------|----------------------|
| WHERE   | Before                        | ❌ No                |
| HAVING  | After                         | ✅ Yes               |
| GROUP BY| N/A (organizes data)          | N/A                 |

---

## 66. **What is a composite key and when should it be used?**

**Answer:**  
A **composite key** is a combination of two or more columns used as the **primary key** of a table. Together, these columns **uniquely identify** each row.

---

### When to Use a Composite Key

- No single column is unique by itself.
- A combination of multiple columns guarantees uniqueness.
- Often used in **many-to-many** relationship tables (junction tables).

---

### Example

```sql
CREATE TABLE CourseEnrollments (
    StudentId INT,
    CourseId INT,
    EnrolledOn DATE,
    PRIMARY KEY (StudentId, CourseId)
);
```

**Explanation:**
- A student can enroll in multiple courses.
- A course can have multiple students.
- The combination of `StudentId` and `CourseId` uniquely identifies each enrollment.

---

### Benefits

- Prevents duplicate entries across multiple fields.
- Enforces real-world uniqueness constraints.
- Saves space compared to using surrogate keys (sometimes).

---

### Caveats

- Can make joins more complex.
- Indexing on multiple columns may require fine-tuning for performance.

---

## 67. **What is a materialized view and how does it differ from a regular view?**

**Answer:**  
A **materialized view** is a database object that stores the result of a query **physically on disk**, unlike a regular view which is a **virtual** table that runs the query each time it is accessed.

---

### Key Differences

| Feature              | View                       | Materialized View           |
|----------------------|----------------------------|-----------------------------|
| Storage              | No (virtual)               | Yes (stored on disk)        |
| Performance          | Slower (recomputes)        | Faster (precomputed)        |
| Data freshness       | Always up-to-date          | Can be stale (requires refresh) |
| Use case             | Lightweight abstraction    | Optimized for heavy queries |

---

### Example – Regular View

```sql
CREATE VIEW ActiveCustomers AS
SELECT * FROM Customers WHERE IsActive = 1;
```

- Query is executed every time the view is accessed.

---

### Example – Materialized View (PostgreSQL)

```sql
CREATE MATERIALIZED VIEW SalesSummary AS
SELECT Region, SUM(Total) AS TotalSales
FROM Orders
GROUP BY Region;
```

```sql
-- Refresh to update the data
REFRESH MATERIALIZED VIEW SalesSummary;
```

---

### Use Cases

- Expensive joins and aggregations
- Dashboards and reports
- Data warehousing

---

## 68. **How do you handle NULL values in queries and constraints?**

**Answer:**  
`NULL` represents **unknown or missing values** in SQL. Handling them properly is critical to maintain data accuracy and avoid logic bugs.

---

### Handling NULLs in Queries

- Use `IS NULL` or `IS NOT NULL` to check for NULLs (not `=` or `!=`).
- Use functions like:
  - `COALESCE(x, fallback)` – returns first non-null value.
  - `ISNULL(x, fallback)` (SQL Server).
  - `IFNULL(x, fallback)` (MySQL).

```sql
-- Replace NULL with 'N/A'
SELECT COALESCE(LastName, 'N/A') AS DisplayName FROM Employees;
```

---

### Example – Filtering NULLs

```sql
SELECT * FROM Orders WHERE ShippedDate IS NULL;
```

---

### NULLs in Constraints

- **Primary keys**: Cannot contain NULLs.
- **Foreign keys**: Can reference NULL if allowed.
- **Unique constraints**: May allow NULLs depending on the RDBMS.

---

### Caution with NULLs in Comparisons

```sql
-- This will not return rows where Discount is NULL
SELECT * FROM Products WHERE Discount <> 0;
```

To include NULLs explicitly:

```sql
SELECT * FROM Products WHERE Discount <> 0 OR Discount IS NULL;
```

---

### Best Practices

- Always check for NULLs explicitly.
- Avoid assuming NULL = 0 or NULL = ''.
- Use default values where possible to prevent NULLs from entering the system.

---

## 69. **What is the difference between scalar functions and table-valued functions?**

**Answer:**  
SQL Server (and other RDBMSs) supports two main types of user-defined functions:

---

### Scalar Functions

- Return a **single value** (e.g., `INT`, `VARCHAR`, `DATE`, etc.)
- Used in SELECT, WHERE, and other clauses
- Accepts parameters and returns a single result

```sql
CREATE FUNCTION GetYearOnly (@date DATE)
RETURNS INT
AS
BEGIN
    RETURN YEAR(@date);
END;
```

```sql
SELECT dbo.GetYearOnly('2024-05-15'); -- Returns: 2024
```

---

### Table-Valued Functions (TVF)

- Return a **table** (set of rows)
- Can be used like a regular table in `FROM` clause
- Useful for encapsulating reusable queries

```sql
CREATE FUNCTION GetHighValueOrders (@minTotal DECIMAL(10,2))
RETURNS TABLE
AS
RETURN (
    SELECT * FROM Orders WHERE TotalAmount > @minTotal
);
```

```sql
SELECT * FROM dbo.GetHighValueOrders(1000);
```

---

### Comparison

| Feature              | Scalar Function          | Table-Valued Function      |
|----------------------|--------------------------|----------------------------|
| Return Type          | Single value             | Table (multiple rows)      |
| Use Case             | Inline calculations      | Reusable query logic       |
| Use in Query         | SELECT/WHERE             | FROM clause                |

---

## 70. **How would you design a schema for a multi-tenant application in SQL?**

**Answer:**  
Multi-tenant applications serve multiple customers (**tenants**) using a shared or isolated database schema. There are 3 common approaches:

---

### 1. **Single Database, Shared Schema**

- All tenants share the same tables.
- Tenant-specific data is separated by a `TenantId` column.

```sql
CREATE TABLE Orders (
    Id INT PRIMARY KEY,
    TenantId INT,
    CustomerId INT,
    Total DECIMAL(10,2)
);
```

- ✅ Easy to scale
- ❌ Requires strict row-level security and indexing

---

### 2. **Single Database, Separate Schema per Tenant**

- Each tenant has their **own schema** within one database.
- E.g., `Tenant1.Orders`, `Tenant2.Orders`

- ✅ Easier logical separation
- ❌ Schema deployment and maintenance become more complex

---

### 3. **Database per Tenant**

- Each tenant gets a **separate physical database**.
- Most secure and isolated.

- ✅ Maximum isolation and customization
- ❌ Expensive to manage and scale

---

### Best Practices

- Always enforce data isolation via `TenantId` filtering
- Use policies, views, or stored procedures to abstract tenant access
- Automate schema updates across tenants
- Use indexed `TenantId` to maintain query performance

---

### Bonus: Add a tenant filter using a view

```sql
CREATE VIEW CurrentTenantOrders AS
SELECT * FROM Orders
WHERE TenantId = CURRENT_TENANT_ID();
```

*(Assumes `CURRENT_TENANT_ID()` is resolved by your app context or session.)*

---

## Modern Language Features

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

---

## Performance and Memory

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

---

## Async & Concurrency

### 40. What does ConfigureAwait(false) actually do?

**Answer:** It tells the awaiter not to capture the current SynchronizationContext/TaskScheduler. Library code thereby resumes on a thread-pool thread, preventing classic UI or ASP.NET deadlocks while also shaving a small performance cost.

**Without ConfigureAwait(false):**
```csharp
public async Task<string> GetDataAsync()
{
    // Captures current SynchronizationContext
    var result = await httpClient.GetStringAsync("https://api.example.com");
    return result; // Resumes on original context (UI thread, ASP.NET request context)
}
```

**With ConfigureAwait(false):**
```csharp
public async Task<string> GetDataAsync()
{
    // Does NOT capture SynchronizationContext
    var result = await httpClient.GetStringAsync("https://api.example.com").ConfigureAwait(false);
    return result; // Resumes on thread pool thread
}
```

**Deadlock Prevention:**
```csharp
// UI Application - potential deadlock
public async Task<string> GetDataFromUI()
{
    // This can deadlock if called from UI thread
    return await GetDataAsync(); // Waits for UI thread, but UI thread is waiting
}

// Library code - safe
public async Task<string> GetDataAsync()
{
    // Always resumes on thread pool, no deadlock
    return await httpClient.GetStringAsync("https://api.example.com").ConfigureAwait(false);
}
```

**When to use:**
- Library code (not UI applications)
- ASP.NET Core (already uses thread pool)
- When you don't need the original context

### 41. Benefits of IAsyncEnumerable<T> and await foreach.

**Answer:** Async streams let a caller process items as they arrive, eliminating full materialisation (List<T>) and allowing back-pressure; each await foreach iteration returns control so other work can proceed, keeping memory low on large result sets or long polls.

**Traditional approach:**
```csharp
// Loads all items into memory
public async Task<List<string>> GetAllItemsAsync()
{
    var items = new List<string>();
    for (int i = 0; i < 1000000; i++)
    {
        var item = await GetItemAsync(i);
        items.Add(item);
    }
    return items; // All items in memory
}
```

**Async streams approach:**
```csharp
// Streams items one by one
public async IAsyncEnumerable<string> GetItemsAsync()
{
    for (int i = 0; i < 1000000; i++)
    {
        var item = await GetItemAsync(i);
        yield return item; // Returns control after each item
    }
}

// Usage
await foreach (var item in GetItemsAsync())
{
    ProcessItem(item); // Process one item at a time
    // Control returns to caller between iterations
}
```

**Back-pressure example:**
```csharp
public async IAsyncEnumerable<int> GenerateNumbersAsync()
{
    for (int i = 0; i < 1000; i++)
    {
        await Task.Delay(100); // Simulate slow generation
        yield return i;
    }
}

// Consumer controls the pace
await foreach (var number in GenerateNumbersAsync())
{
    await ProcessNumberAsync(number); // Slow processing
    // Generator waits until consumer is ready
}
```

### 42. Why was IAsyncDisposable added?

**Answer:** Some resources (Sockets, channels) need asynchronous teardown. Implementing DisposeAsync returns a ValueTask so cleanup can itself await I/O. The await using syntax ensures callers don't forget to await that asynchronous dispose path.

**Traditional IDisposable:**
```csharp
public class DatabaseConnection : IDisposable
{
    public void Dispose()
    {
        // Synchronous cleanup
        CloseConnection();
    }
}

// Usage
using (var connection = new DatabaseConnection())
{
    // Use connection
} // Dispose called synchronously
```

**IAsyncDisposable:**
```csharp
public class AsyncDatabaseConnection : IAsyncDisposable
{
    public async ValueTask DisposeAsync()
    {
        // Asynchronous cleanup
        await CloseConnectionAsync();
    }
}

// Usage with await using
await using (var connection = new AsyncDatabaseConnection())
{
    // Use connection
} // DisposeAsync called asynchronously
```

**Real-world example:**
```csharp
public class WebSocketHandler : IAsyncDisposable
{
    private WebSocket _webSocket;
    
    public async ValueTask DisposeAsync()
    {
        if (_webSocket != null)
        {
            // Asynchronous cleanup
            await _webSocket.CloseAsync(WebSocketCloseStatus.NormalClosure, 
                                       "Disposing", CancellationToken.None);
            _webSocket.Dispose();
        }
    }
}

// Usage
await using var handler = new WebSocketHandler();
// WebSocket will be properly closed asynchronously
```

**Benefits:**
- Proper async resource cleanup
- Prevents resource leaks
- Enables async I/O during disposal
- Compiler enforces await using

---

## Architecture & Patterns

### 43. Illustrate SOLID with dependency injection in .NET.

**Answer:** Single-Responsibility—keep InvoiceService lean and inject ILogger. O/C—new discount rules via injected IDiscountStrategy. L—abstract base types so derived mocks substitute cleanly. Registration (services.AddTransient<IInvoiceService, InvoiceService>();) wires the abstractions at composition-root, letting tests replace them with fakes.

**Single Responsibility Principle:**
```csharp
// Bad: Multiple responsibilities
public class InvoiceService
{
    public void ProcessInvoice(Invoice invoice)
    {
        // Business logic
        CalculateTotal(invoice);
        
        // Logging (separate responsibility)
        File.WriteAllText("log.txt", $"Invoice {invoice.Id} processed");
        
        // Database access (separate responsibility)
        using var context = new InvoiceContext();
        context.Invoices.Add(invoice);
        context.SaveChanges();
    }
}

// Good: Single responsibility with DI
public class InvoiceService
{
    private readonly ILogger<InvoiceService> _logger;
    private readonly IInvoiceRepository _repository;
    
    public InvoiceService(ILogger<InvoiceService> logger, IInvoiceRepository repository)
    {
        _logger = logger;
        _repository = repository;
    }
    
    public void ProcessInvoice(Invoice invoice)
    {
        // Only business logic
        CalculateTotal(invoice);
        _repository.Save(invoice);
        _logger.LogInformation("Invoice {InvoiceId} processed", invoice.Id);
    }
}
```

**Open/Closed Principle:**
```csharp
// Strategy pattern with DI
public interface IDiscountStrategy
{
    decimal CalculateDiscount(Order order);
}

public class PercentageDiscountStrategy : IDiscountStrategy
{
    private readonly decimal _percentage;
    
    public PercentageDiscountStrategy(decimal percentage) => _percentage = percentage;
    
    public decimal CalculateDiscount(Order order) => order.Total * _percentage;
}

public class OrderService
{
    private readonly IDiscountStrategy _discountStrategy;
    
    public OrderService(IDiscountStrategy discountStrategy)
    {
        _discountStrategy = discountStrategy;
    }
    
    public decimal CalculateFinalPrice(Order order)
    {
        var discount = _discountStrategy.CalculateDiscount(order);
        return order.Total - discount;
    }
}

// Registration
services.AddTransient<IDiscountStrategy, PercentageDiscountStrategy>();
services.AddTransient<OrderService>();
```

**Liskov Substitution Principle:**
```csharp
// Base abstraction
public interface IUserRepository
{
    Task<User> GetByIdAsync(int id);
    Task SaveAsync(User user);
}

// Real implementation
public class SqlUserRepository : IUserRepository
{
    public async Task<User> GetByIdAsync(int id) { /* SQL implementation */ }
    public async Task SaveAsync(User user) { /* SQL implementation */ }
}

// Mock implementation for testing
public class MockUserRepository : IUserRepository
{
    public async Task<User> GetByIdAsync(int id) { /* Mock implementation */ }
    public async Task SaveAsync(User user) { /* Mock implementation */ }
}

// Both can be substituted
services.AddTransient<IUserRepository, SqlUserRepository>(); // Production
services.AddTransient<IUserRepository, MockUserRepository>(); // Testing
```

### 44. When and how to use Repository + Unit of Work with EF Core?

**Answer:** A repository hides LINQ-to-Entities queries behind an interface, enabling in-memory or mock implementations; the Unit of Work (DbContext or wrapper) coordinates multiple repositories under one transaction. It's most useful when cross-aggregate consistency or swap-out storage is required.

**Repository Pattern:**
```csharp
public interface IUserRepository
{
    Task<User> GetByIdAsync(int id);
    Task<IEnumerable<User>> GetAllAsync();
    Task AddAsync(User user);
    Task UpdateAsync(User user);
    Task DeleteAsync(int id);
}

public class UserRepository : IUserRepository
{
    private readonly ApplicationDbContext _context;
    
    public UserRepository(ApplicationDbContext context)
    {
        _context = context;
    }
    
    public async Task<User> GetByIdAsync(int id)
    {
        return await _context.Users
            .Include(u => u.Orders)
            .FirstOrDefaultAsync(u => u.Id == id);
    }
    
    public async Task<IEnumerable<User>> GetAllAsync()
    {
        return await _context.Users.ToListAsync();
    }
    
    public async Task AddAsync(User user)
    {
        await _context.Users.AddAsync(user);
    }
    
    public async Task UpdateAsync(User user)
    {
        _context.Users.Update(user);
        await Task.CompletedTask;
    }
    
    public async Task DeleteAsync(int id)
    {
        var user = await GetByIdAsync(id);
        if (user != null)
        {
            _context.Users.Remove(user);
        }
    }
}
```

**Unit of Work Pattern:**
```csharp
public interface IUnitOfWork : IDisposable
{
    IUserRepository Users { get; }
    IOrderRepository Orders { get; }
    Task<int> SaveChangesAsync();
}

public class UnitOfWork : IUnitOfWork
{
    private readonly ApplicationDbContext _context;
    private IUserRepository _userRepository;
    private IOrderRepository _orderRepository;
    
    public UnitOfWork(ApplicationDbContext context)
    {
        _context = context;
    }
    
    public IUserRepository Users => 
        _userRepository ??= new UserRepository(_context);
    
    public IOrderRepository Orders => 
        _orderRepository ??= new OrderRepository(_context);
    
    public async Task<int> SaveChangesAsync()
    {
        return await _context.SaveChangesAsync();
    }
    
    public void Dispose()
    {
        _context?.Dispose();
    }
}
```

**Usage with Transaction:**
```csharp
public class UserService
{
    private readonly IUnitOfWork _unitOfWork;
    
    public UserService(IUnitOfWork unitOfWork)
    {
        _unitOfWork = unitOfWork;
    }
    
    public async Task CreateUserWithOrderAsync(User user, Order order)
    {
        // Both operations in same transaction
        await _unitOfWork.Users.AddAsync(user);
        await _unitOfWork.Orders.AddAsync(order);
        
        // Single commit
        await _unitOfWork.SaveChangesAsync();
    }
}

// Registration
services.AddScoped<IUnitOfWork, UnitOfWork>();
services.AddScoped<IUserRepository, UserRepository>();
services.AddScoped<IOrderRepository, OrderRepository>();
```

### 45. Outline Clean Architecture layers.

**Answer:** Entities (domain models) have no dependencies. Use-cases/Application reference entities only. Interface adapters (controllers, presenters, gateways) map to infrastructure. The outer Infrastructure ring (EF Core, Web, File I/O) depends inward, never the reverse; this allows swapping SQL for NoSQL without touching business rules.

**Layer Structure:**
```
┌─────────────────────────────────────┐
│           Presentation              │ ← Controllers, Views, APIs
├─────────────────────────────────────┤
│           Application               │ ← Use Cases, Services
├─────────────────────────────────────┤
│             Domain                  │ ← Entities, Value Objects
├─────────────────────────────────────┤
│          Infrastructure             │ ← Database, External APIs
└─────────────────────────────────────┘
```

**Domain Layer (No Dependencies):**
```csharp
// Entities
public class User
{
    public int Id { get; private set; }
    public string Name { get; private set; }
    public string Email { get; private set; }
    
    public User(string name, string email)
    {
        Name = name;
        Email = email;
    }
    
    public void UpdateName(string newName)
    {
        if (string.IsNullOrEmpty(newName))
            throw new ArgumentException("Name cannot be empty");
        
        Name = newName;
    }
}

// Value Objects
public record EmailAddress
{
    public string Value { get; }
    
    public EmailAddress(string value)
    {
        if (!IsValidEmail(value))
            throw new ArgumentException("Invalid email format");
        
        Value = value;
    }
    
    private static bool IsValidEmail(string email) => 
        email.Contains("@") && email.Contains(".");
}
```

**Application Layer (Depends on Domain):**
```csharp
// Use Cases
public interface ICreateUserUseCase
{
    Task<User> ExecuteAsync(CreateUserRequest request);
}

public class CreateUserUseCase : ICreateUserUseCase
{
    private readonly IUserRepository _userRepository;
    
    public CreateUserUseCase(IUserRepository userRepository)
    {
        _userRepository = userRepository;
    }
    
    public async Task<User> ExecuteAsync(CreateUserRequest request)
    {
        var user = new User(request.Name, request.Email);
        await _userRepository.AddAsync(user);
        return user;
    }
}

// DTOs
public record CreateUserRequest(string Name, string Email);
```

**Infrastructure Layer (Depends on Application):**
```csharp
// Repository Implementation
public class EfUserRepository : IUserRepository
{
    private readonly ApplicationDbContext _context;
    
    public EfUserRepository(ApplicationDbContext context)
    {
        _context = context;
    }
    
    public async Task<User> AddAsync(User user)
    {
        var entity = new UserEntity
        {
            Name = user.Name,
            Email = user.Email
        };
        
        _context.Users.Add(entity);
        await _context.SaveChangesAsync();
        
        return new User(entity.Name, entity.Email) { Id = entity.Id };
    }
}

// Database Context
public class ApplicationDbContext : DbContext
{
    public DbSet<UserEntity> Users { get; set; }
    
    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<UserEntity>(entity =>
        {
            entity.HasKey(e => e.Id);
            entity.Property(e => e.Name).IsRequired();
            entity.Property(e => e.Email).IsRequired();
        });
    }
}
```

**Presentation Layer (Depends on Application):**
```csharp
// API Controller
[ApiController]
[Route("api/[controller]")]
public class UsersController : ControllerBase
{
    private readonly ICreateUserUseCase _createUserUseCase;
    
    public UsersController(ICreateUserUseCase createUserUseCase)
    {
        _createUserUseCase = createUserUseCase;
    }
    
    [HttpPost]
    public async Task<IActionResult> CreateUser([FromBody] CreateUserRequest request)
    {
        try
        {
            var user = await _createUserUseCase.ExecuteAsync(request);
            return Ok(user);
        }
        catch (ArgumentException ex)
        {
            return BadRequest(ex.Message);
        }
    }
}
```

**Benefits:**
- Business logic is isolated and testable
- Infrastructure can be swapped without affecting domain
- Dependencies flow inward
- Easy to test each layer independently

---

## Framework-Specific

### 46. What is MVC (Model-View-Controller)?

**Answer:** MVC is a software design pattern that separates an application into three components:

- **Model**: Represents the data and business logic.
- **View**: Handles the presentation layer.
- **Controller**: Manages user input and updates the model.

### Example: A Simple MVC Controller in ASP.NET Core
```csharp
public class HomeController : Controller
{
    public IActionResult Index()
    {
        return View();
    }
}
```

### 47. Can you explain the difference between Razor Pages and MVC in ASP.NET Core?

- **MVC** uses a Controller to handle requests, while **Razor Pages** has built-in page handlers (`OnGet`, `OnPost`).
- Razor Pages is more suitable for simple, page-focused applications, whereas MVC is better for larger applications.

### Example: Razor Page Handler
```csharp
public class IndexModel : PageModel
{
    public void OnGet()
    {
        // Handle GET request
    }
}
```

### 48. How do you perform validations in ASP.NET Core?

ASP.NET Core provides validation using **Data Annotations** and **Fluent Validation**.

### Example: Using Data Annotations
```csharp
public class UserModel
{
    [Required]
    [EmailAddress]
    public string Email { get; set; }

    [Required]
    [MinLength(6)]
    public string Password { get; set; }
}
```

### 49. Describe SignalR and its use cases.

SignalR is a real-time communication library in ASP.NET Core that enables WebSockets for interactive web applications.

### Example: SignalR Hub
```csharp
public class ChatHub : Hub
{
    public async Task SendMessage(string user, string message)
    {
        await Clients.All.SendAsync("ReceiveMessage", user, message);
    }
}
```

### 50. What are the benefits of using Blazor over traditional web technologies?

Blazor allows building web applications using **C# and .NET** instead of JavaScript.

### Example: Blazor Component
```csharp
@code {
    string message = "Hello, Blazor!";
}
<p>@message</p>
```

### 51. How do you implement Web API versioning in ASP.NET Core?

API versioning ensures backward compatibility for REST APIs.

### Example: Using API Versioning Middleware
```csharp
services.AddApiVersioning(o =>
{
    o.ReportApiVersions = true;
    o.AssumeDefaultVersionWhenUnspecified = true;
    o.DefaultApiVersion = new ApiVersion(1, 0);
});
```

### 52. Explain the role of `IApplicationBuilder` in ASP.NET Core.

`IApplicationBuilder` is used in `Startup.Configure()` to define the middleware pipeline.

### Example:
```csharp
public void Configure(IApplicationBuilder app)
{
    app.UseRouting();
    app.UseAuthorization();
    app.UseEndpoints(endpoints => endpoints.MapControllers());
}
```

### 53. What are Areas in ASP.NET Core and how do you use them?

Areas help organize large MVC applications by grouping controllers, views, and models.

### Example: Defining an Area
```csharp
[Area("Admin")]
public class DashboardController : Controller
{
    public IActionResult Index() => View();
}
```

### 54. How do you manage sessions in ASP.NET Core applications?

ASP.NET Core provides session state management using `ISession`.

### Example:
```csharp
services.AddSession();

app.UseSession();

HttpContext.Session.SetString("User", "Admin");
string user = HttpContext.Session.GetString("User");
```

### 55. Describe how to implement caching in ASP.NET Core.

ASP.NET Core supports memory caching and distributed caching.

### Example: In-Memory Caching
```csharp
services.AddMemoryCache();

public class MyService
{
    private readonly IMemoryCache _cache;
    public MyService(IMemoryCache cache) { _cache = cache; }

    public string GetData()
    {
        return _cache.GetOrCreate("cachedData", entry => "Hello, Cache!"); 
    }
}
```

### 56. Minimal APIs vs. MVC controllers in ASP.NET Core 8.

**Answer:** Minimal APIs offer function-style routing, lower allocations and slightly faster throughput (~5-8 %) because they skip model-binding metadata; they fit micro-services and prototyping. MVC adds filters, model validation, and full view support—better for large teams needing separation of concerns.

**Minimal API Example:**
```csharp
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

// Minimal API - function-style routing
app.MapGet("/users/{id}", async (int id, IUserService userService) =>
{
    var user = await userService.GetByIdAsync(id);
    return user != null ? Results.Ok(user) : Results.NotFound();
});

app.MapPost("/users", async (CreateUserRequest request, IUserService userService) =>
{
    var user = await userService.CreateAsync(request);
    return Results.Created($"/users/{user.Id}", user);
});

app.Run();
```

**MVC Controller Example:**
```csharp
[ApiController]
[Route("api/[controller]")]
public class UsersController : ControllerBase
{
    private readonly IUserService _userService;
    
    public UsersController(IUserService userService)
    {
        _userService = userService;
    }
    
    [HttpGet("{id}")]
    public async Task<IActionResult> GetById(int id)
    {
        var user = await _userService.GetByIdAsync(id);
        return user != null ? Ok(user) : NotFound();
    }
    
    [HttpPost]
    public async Task<IActionResult> Create([FromBody] CreateUserRequest request)
    {
        var user = await _userService.CreateAsync(request);
        return CreatedAtAction(nameof(GetById), new { id = user.Id }, user);
    }
}
```

**Comparison:**
| Feature | Minimal APIs | MVC Controllers |
|---------|--------------|-----------------|
| Performance | Faster (~5-8%) | Slightly slower |
| Memory usage | Lower allocations | Higher allocations |
| Model binding | Manual | Automatic |
| Filters | Limited | Full support |
| Validation | Manual | Automatic |
| Views | No | Yes |
| Best for | Microservices, prototyping | Large applications |

### 57. Why is middleware order critical?

**Answer:** The pipeline is first-in-first-executed. Place global exception/logging first, UseStaticFiles early, UseRouting then auth, followed by UseAuthorization, finally UseEndpoints. Mis-ordering can expose static files without auth or miss routing entirely.

**Correct Middleware Order:**
```csharp
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    // 1. Exception handling first
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }
    else
    {
        app.UseExceptionHandler("/Error");
        app.UseHsts();
    }
    
    // 2. HTTPS redirection
    app.UseHttpsRedirection();
    
    // 3. Static files (before auth to allow public access)
    app.UseStaticFiles();
    
    // 4. Routing
    app.UseRouting();
    
    // 5. Authentication
    app.UseAuthentication();
    
    // 6. Authorization
    app.UseAuthorization();
    
    // 7. Endpoints last
    app.UseEndpoints(endpoints =>
    {
        endpoints.MapControllers();
        endpoints.MapRazorPages();
    });
}
```

**Common Mistakes:**
```csharp
// WRONG: Auth before routing
app.UseAuthentication(); // Won't work properly
app.UseRouting();

// WRONG: Static files after auth
app.UseAuthentication();
app.UseStaticFiles(); // Files might be blocked

// WRONG: Endpoints before routing
app.UseEndpoints(endpoints => endpoints.MapControllers());
app.UseRouting(); // Too late!
```

**Why Order Matters:**
- **Exception handling** must be first to catch all errors
- **Static files** should be before auth for public resources
- **Routing** must come before auth/authorization
- **Authentication** must come before authorization
- **Endpoints** must be last to handle the request

### 58. How do you secure an API with JWT in ASP.NET Core?

**Answer:** Add authentication services: services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme).AddJwtBearer(opts => { opts.Authority = "..."; opts.Audience = "..."; }); then app.UseAuthentication(); app.UseAuthorization();. The middleware validates issuer, audience and the RS256 signature for every inbound token, enabling stateless auth.

**JWT Configuration:**
```csharp
// Program.cs or Startup.cs
builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
    .AddJwtBearer(options =>
    {
        options.Authority = "https://your-auth-server.com";
        options.Audience = "your-api-audience";
        options.RequireHttpsMetadata = true;
        options.TokenValidationParameters = new TokenValidationParameters
        {
            ValidateIssuer = true,
            ValidateAudience = true,
            ValidateLifetime = true,
            ValidateIssuerSigningKey = true,
            ValidIssuer = "https://your-auth-server.com",
            ValidAudience = "your-api-audience"
        };
    });

builder.Services.AddAuthorization(options =>
{
    options.AddPolicy("AdminOnly", policy =>
        policy.RequireRole("Admin"));
    
    options.AddPolicy("UserAccess", policy =>
        policy.RequireClaim("scope", "api.read"));
});

var app = builder.Build();

// Middleware order is important
app.UseAuthentication();
app.UseAuthorization();
```

**Protected Controller:**
```csharp
[ApiController]
[Route("api/[controller]")]
[Authorize] // Requires valid JWT
public class SecureController : ControllerBase
{
    [HttpGet]
    public IActionResult Get()
    {
        // Access user claims
        var userId = User.FindFirst(ClaimTypes.NameIdentifier)?.Value;
        var email = User.FindFirst(ClaimTypes.Email)?.Value;
        
        return Ok(new { message = "Secure data", userId, email });
    }
    
    [HttpGet("admin")]
    [Authorize(Policy = "AdminOnly")] // Requires Admin role
    public IActionResult AdminOnly()
    {
        return Ok("Admin access granted");
    }
    
    [HttpGet("user")]
    [Authorize(Policy = "UserAccess")] // Requires specific claim
    public IActionResult UserAccess()
    {
        return Ok("User access granted");
    }
}
```

**JWT Token Structure:**
```json
{
  "header": {
    "alg": "RS256",
    "typ": "JWT"
  },
  "payload": {
    "sub": "1234567890",
    "name": "John Doe",
    "email": "john@example.com",
    "role": "Admin",
    "scope": "api.read api.write",
    "iat": 1516239022,
    "exp": 1516242622,
    "iss": "https://your-auth-server.com",
    "aud": "your-api-audience"
  },
  "signature": "RS256 signature..."
}
```

**Security Best Practices:**
- Use HTTPS in production
- Set appropriate token expiration
- Validate all required claims
- Use strong signing keys
- Implement token refresh mechanism
- Log authentication events

---

## Testing & Best Practices

### 59. What is Unit Testing in .NET?

Unit testing is the practice of testing individual components of an application in isolation.

### Example: NUnit Unit Test
```csharp
[Test]
public void TestSum()
{
    int result = Calculator.Sum(2, 3);
    Assert.AreEqual(5, result);
}
```

### 60. How do you mock dependencies in unit tests using .NET?

Mocking is used to simulate dependencies in unit tests using **Moq**.

### Example:
```csharp
var mockRepo = new Mock<IRepository>();
mockRepo.Setup(repo => repo.GetData()).Returns("Mock Data");
```

### 61. Can you explain SOLID principles?

**SOLID** is a set of five principles for writing maintainable code:

1. **S**ingle Responsibility Principle
2. **O**pen/Closed Principle
3. **L**iskov Substitution Principle
4. **I**nterface Segregation Principle
5. **D**ependency Inversion Principle

### 62. What is Continuous Integration/Continuous Deployment (CI/CD)?

CI/CD automates code integration, testing, and deployment.

### Example: GitHub Actions for CI/CD
```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v2
      - name: Build and Test
        run: dotnet test
```

### 63. How do you ensure your C# code is secure?

Writing secure C# code requires following best practices to prevent vulnerabilities such as SQL injection, cross-site scripting (XSS), and unauthorized access.

### Key Security Measures:
- **Use parameterized queries** to prevent SQL injection.
- **Hash and salt passwords** using `BCrypt` or `PBKDF2`.
- **Enable HTTPS** to encrypt communication.
- **Validate user input** to prevent injection attacks.
- **Use dependency injection (DI)** to avoid hardcoded secrets.

### Example: Preventing SQL Injection
```csharp
using System.Data.SqlClient;

public void GetUser(int userId)
{
    using (SqlConnection conn = new SqlConnection("connectionString"))
    {
        string query = "SELECT * FROM Users WHERE Id = @userId";
        using (SqlCommand cmd = new SqlCommand(query, conn))
        {
            cmd.Parameters.AddWithValue("@userId", userId);
            conn.Open();
            var reader = cmd.ExecuteReader();
            while (reader.Read())
            {
                Console.WriteLine(reader["Name"]);
            }
        }
    }
}
```

### 64. What are some common performance issues in .NET applications and how do you address them?

Performance issues in .NET applications often arise due to inefficient memory usage, slow database queries, or excessive allocations.

### Common Performance Issues and Fixes:
- **Memory Leaks** → Use `IDisposable` and `using` statements.
- **Slow Queries** → Optimize SQL queries and indexing.
- **Excessive Object Allocations** → Use object pooling and struct types.

### Example: Using Caching to Improve Performance
```csharp
public class DataService
{
    private readonly IMemoryCache _cache;
    public DataService(IMemoryCache cache)
    {
        _cache = cache;
    }

    public string GetData()
    {
        return _cache.GetOrCreate("cachedData", entry =>
        {
            entry.AbsoluteExpirationRelativeToNow = TimeSpan.FromMinutes(5);
            return "Cached Data";
        });
    }
}
```

### 65. Describe the Repository pattern and its benefits.

The **Repository Pattern** abstracts the data layer, providing a clean way to manage database operations.

### Benefits:
- **Separation of concerns** → Keeps data access logic separate.
- **Easier testing** → Allows mocking of database operations.
- **Code reusability** → Centralizes data access logic.

### Example: Repository Pattern in ASP.NET Core
```csharp
public interface IUserRepository
{
    IEnumerable<User> GetAllUsers();
    User GetUserById(int id);
}

public class UserRepository : IUserRepository
{
    private readonly AppDbContext _context;
    public UserRepository(AppDbContext context) { _context = context; }

    public IEnumerable<User> GetAllUsers() => _context.Users.ToList();

    public User GetUserById(int id) => _context.Users.Find(id);
}
```

### 66. How do you handle database migrations in Entity Framework?

Migrations in Entity Framework allow changes to the database schema while preserving existing data.

### Steps to Apply Migrations:
1. **Add a new migration:**
   ```shell
   dotnet ef migrations add InitialCreate
   ```
2. **Apply the migration to the database:**
   ```shell
   dotnet ef database update
   ```

### Example: Defining a Model with Migrations
```csharp
public class User
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Email { get; set; }
}
```

### 67. What tools do you use for debugging and profiling .NET applications?

Effective debugging and profiling tools help identify performance bottlenecks and runtime errors.

### Popular Tools:
- **Visual Studio Debugger** → Step-through debugging.
- **dotTrace** → Identifies CPU-intensive operations.
- **BenchmarkDotNet** → Measures code performance.
- **dotMemory** → Finds memory leaks.

### Example: Using BenchmarkDotNet to Measure Performance
```csharp
[MemoryDiagnoser]
public class PerformanceTests
{
    [Benchmark]
    public void TestMethod()
    {
        var list = new List<int>();
        for (int i = 0; i < 1000; i++)
        {
            list.Add(i);
        }
    }
}
```

### 68. How do you stay updated with the latest .NET technologies and practices?

Staying current with .NET advancements ensures that you use the best tools and frameworks.

### Recommended Ways to Stay Updated:
- **Follow Microsoft's .NET Blog** → [https://devblogs.microsoft.com/dotnet/](https://devblogs.microsoft.com/dotnet/)
- **Attend Conferences/Webinars** → .NET Conf, Microsoft Build
- **Join Online Communities** → GitHub, Stack Overflow, Twitter

### 69. How do xUnit and Moq work together in unit tests?

**Answer:** Arrange mocks: var repo = new Mock<IRepo>(); repo.Setup(r => r.Add(It.IsAny<Item>()));. Act: call SUT. Assert: repo.Verify(r => r.Add(It.Is<Item>(i => i.Id==1)), Times.Once); then use xUnit's [Fact] and fluent assertions. This isolates code and keeps tests fast (<10 ms typical).

**Complete Unit Test Example:**
```csharp
public class UserServiceTests
{
    [Fact]
    public async Task CreateUser_ValidUser_ShouldSaveToRepository()
    {
        // Arrange
        var mockRepo = new Mock<IUserRepository>();
        var mockLogger = new Mock<ILogger<UserService>>();
        var userService = new UserService(mockRepo.Object, mockLogger.Object);
        
        var createRequest = new CreateUserRequest("John", "john@example.com");
        var expectedUser = new User("John", "john@example.com") { Id = 1 };
        
        mockRepo.Setup(r => r.AddAsync(It.IsAny<User>()))
                .ReturnsAsync(expectedUser);
        
        // Act
        var result = await userService.CreateUserAsync(createRequest);
        
        // Assert
        Assert.NotNull(result);
        Assert.Equal("John", result.Name);
        Assert.Equal("john@example.com", result.Email);
        
        mockRepo.Verify(r => r.AddAsync(It.Is<User>(u => 
            u.Name == "John" && u.Email == "john@example.com")), Times.Once);
    }
    
    [Fact]
    public async Task CreateUser_InvalidEmail_ShouldThrowException()
    {
        // Arrange
        var mockRepo = new Mock<IUserRepository>();
        var mockLogger = new Mock<ILogger<UserService>>();
        var userService = new UserService(mockRepo.Object, mockLogger.Object);
        
        var createRequest = new CreateUserRequest("John", "invalid-email");
        
        // Act & Assert
        await Assert.ThrowsAsync<ArgumentException>(() => 
            userService.CreateUserAsync(createRequest));
        
        mockRepo.Verify(r => r.AddAsync(It.IsAny<User>()), Times.Never);
    }
}
```

**Moq Setup Patterns:**
```csharp
// Setup return values
mockRepo.Setup(r => r.GetByIdAsync(1))
        .ReturnsAsync(new User("John", "john@example.com"));

// Setup with parameters
mockRepo.Setup(r => r.GetByEmailAsync(It.IsAny<string>()))
        .ReturnsAsync((string email) => new User("John", email));

// Setup exceptions
mockRepo.Setup(r => r.GetByIdAsync(-1))
        .ThrowsAsync(new ArgumentException("Invalid ID"));

// Setup callbacks
mockRepo.Setup(r => r.AddAsync(It.IsAny<User>()))
        .Callback<User>(user => user.Id = 1)
        .ReturnsAsync((User user) => user);
```

**xUnit Attributes:**
```csharp
[Fact] // Simple test
public void SimpleTest() { }

[Theory] // Parameterized test
[InlineData(1, 2, 3)]
[InlineData(0, 0, 0)]
[InlineData(-1, 1, 0)]
public void AddTest(int a, int b, int expected)
{
    var result = Calculator.Add(a, b);
    Assert.Equal(expected, result);
}

[Fact(Skip = "Temporarily disabled")] // Skip test
public void SkippedTest() { }
```

### 70. Purpose of WebApplicationFactory in integration tests.

**Answer:** WebApplicationFactory<TEntry> spins an in-memory TestServer with your real startup, letting you perform end-to-end HTTP calls without deploying or binding ports. It honors DI, middleware, filters and routing exactly as in production.

**Integration Test Example:**
```csharp
public class UserControllerIntegrationTests : IClassFixture<WebApplicationFactory<Program>>
{
    private readonly WebApplicationFactory<Program> _factory;
    private readonly HttpClient _client;
    
    public UserControllerIntegrationTests(WebApplicationFactory<Program> factory)
    {
        _factory = factory;
        _client = factory.CreateClient();
    }
    
    [Fact]
    public async Task GetUsers_ShouldReturnUsers()
    {
        // Act
        var response = await _client.GetAsync("/api/users");
        
        // Assert
        response.EnsureSuccessStatusCode();
        var content = await response.Content.ReadAsStringAsync();
        var users = JsonSerializer.Deserialize<List<User>>(content);
        
        Assert.NotNull(users);
        Assert.NotEmpty(users);
    }
    
    [Fact]
    public async Task CreateUser_ValidUser_ShouldReturnCreated()
    {
        // Arrange
        var user = new CreateUserRequest("John", "john@example.com");
        var json = JsonSerializer.Serialize(user);
        var content = new StringContent(json, Encoding.UTF8, "application/json");
        
        // Act
        var response = await _client.PostAsync("/api/users", content);
        
        // Assert
        Assert.Equal(HttpStatusCode.Created, response.StatusCode);
        Assert.NotNull(response.Headers.Location);
    }
}
```

**Custom WebApplicationFactory:**
```csharp
public class CustomWebApplicationFactory : WebApplicationFactory<Program>
{
    protected override void ConfigureWebHost(IWebHostBuilder builder)
    {
        builder.ConfigureServices(services =>
        {
            // Replace real database with in-memory
            var descriptor = services.SingleOrDefault(
                d => d.ServiceType == typeof(DbContextOptions<ApplicationDbContext>));
            
            if (descriptor != null)
            {
                services.Remove(descriptor);
            }
            
            services.AddDbContext<ApplicationDbContext>(options =>
            {
                options.UseInMemoryDatabase("TestDb");
            });
            
            // Replace external services with mocks
            services.AddScoped<IEmailService, MockEmailService>();
        });
    }
}
```

**Benefits:**
- Tests real HTTP pipeline
- Validates routing and middleware
- Tests authentication/authorization
- No external dependencies
- Fast execution

### 71. What does dotnet publish single-file/self-contained achieve?

**Answer:** dotnet publish -c Release -p:PublishSingleFile=true -p:SelfContained=true bundles IL, native runtime and dependencies into one executable. Useful for container images or XCOPY deploy; IL trimming (AOT-trim) further removes unused framework code to shrink size.

**Publishing Options:**
```bash
# Framework-dependent (requires .NET runtime installed)
dotnet publish -c Release

# Self-contained (includes runtime)
dotnet publish -c Release -r win-x64 --self-contained true

# Single file (everything in one executable)
dotnet publish -c Release -r win-x64 --self-contained true -p:PublishSingleFile=true

# With trimming (remove unused code)
dotnet publish -c Release -r win-x64 --self-contained true -p:PublishSingleFile=true -p:PublishTrimmed=true

# AOT compilation (native code)
dotnet publish -c Release -r win-x64 --self-contained true -p:PublishAOT=true
```

**Project File Configuration:**
```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net8.0</TargetFramework>
    <PublishSingleFile>true</PublishSingleFile>
    <SelfContained>true</SelfContained>
    <RuntimeIdentifier>win-x64</RuntimeIdentifier>
    <PublishTrimmed>true</PublishTrimmed>
    <TrimMode>link</TrimMode>
  </PropertyGroup>
</Project>
```

**Size Comparison:**
```bash
# Framework-dependent
dotnet publish -c Release
# Size: ~5-10 MB

# Self-contained
dotnet publish -c Release -r win-x64 --self-contained true
# Size: ~50-100 MB

# Single file + trimming
dotnet publish -c Release -r win-x64 --self-contained true -p:PublishSingleFile=true -p:PublishTrimmed=true
# Size: ~30-60 MB

# AOT compilation
dotnet publish -c Release -r win-x64 --self-contained true -p:PublishAOT=true
# Size: ~20-40 MB
```

**Use Cases:**
- **Container images** - Single executable reduces image size
- **XCOPY deployment** - No installation required
- **Embedded systems** - Minimal footprint
- **CI/CD pipelines** - Self-contained artifacts

**Benefits:**
- No runtime installation required
- Faster startup (AOT)
- Smaller deployment size (trimming)
- Better security (fewer dependencies)
