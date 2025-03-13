# Senior .NET Developer Interview Preparation

## Table of Contents
1. [Core .NET & C# Concepts](#core-net--c-concepts)
2. [Object-Oriented Programming (OOP)](#object-oriented-programming-oop)
3. [SOLID Principles & Design Patterns](#solid-principles--design-patterns)
4. [Dependency Injection, Unit Testing (xUnit/NUnit/Moq)](#dependency-injection-unit-testing-xunitnunitmoq)
5. [Async/Await, Multithreading](#asyncawait-multithreading)
6. [.NET Core & .NET 6/7 Updates](#net-core--net-67-updates)

## Core .NET & C# Concepts

### .NET Framework vs .NET Core vs .NET 5/6/7
.NET Framework is the original implementation of .NET, primarily for Windows. .NET Core is a cross-platform, high-performance, and open-source framework. .NET 5/6/7 unify the platforms, bringing new features and improvements.

**Advantages:**
- **Cross-Platform:** Allows applications to run on Windows, macOS, and Linux.
- **Performance:** Improved performance and scalability.
- **Unified Development:** Single platform for web, desktop, mobile, cloud, and IoT applications.

**Example:**
```csharp
// .NET Core Example: Cross-platform console application
using System;

namespace HelloWorld
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

### CLR (Common Language Runtime)
The CLR provides services like memory management, garbage collection, security, and exception handling. It compiles the Intermediate Language (IL) code to native machine code.

**Advantages:**
- **Memory Management:** Automatic memory management through garbage collection.
- **Security:** Enforces code access security and verification.
- **Interoperability:** Allows interaction between different .NET languages.

### CTS (Common Type System)
CTS defines how types are declared, used, and managed. It ensures that objects written in different .NET languages can interact with each other.

**Advantages:**
- **Language Interoperability:** Ensures that types are compatible across different languages.
- **Consistency:** Provides a consistent object-oriented programming model.

### Garbage Collection
Garbage Collection (GC) automatically manages memory by deallocating unused objects, reducing memory leaks and fragmentation. It uses generations to optimize performance.

**Advantages:**
- **Automatic Memory Management:** Reduces memory leaks and manual memory management errors.
- **Performance Optimization:** Uses generational approach to optimize performance.

**Example:**
```csharp
// Example of forcing garbage collection
using System;

class Program
{
    static void Main()
    {
        Console.WriteLine("Start of Main");
        GC.Collect();
        Console.WriteLine("End of Main");
    }
}
```

### LINQ (Language Integrated Query)
LINQ allows querying collections in a concise, readable manner using syntax integrated into C#. It supports querying objects, databases, XML, and more.

**Advantages:**
- **Readability:** Provides a concise and readable syntax for querying.
- **Type Safety:** Ensures type safety at compile time.
- **Flexibility:** Can be used with various data sources.

**Example:**
```csharp
using System;
using System.Linq;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };
        var evenNumbers = from num in numbers
                          where num % 2 == 0
                          select num;

        foreach (var num in evenNumbers)
        {
            Console.WriteLine(num);
        }
    }
}
```

### C# Language Features

#### Delegates
Delegates are type-safe function pointers that allow methods to be passed as parameters. They are used to define callback methods and implement event handling.

**Advantages:**
- **Flexibility:** Allows methods to be passed as parameters.
- **Type Safety:** Ensures type safety at compile time.

**Example:**
```csharp
public delegate void MyDelegate(string message);

public class Program
{
    public static void Main()
    {
        MyDelegate del = new MyDelegate(PrintMessage);
        del("Hello, World!");

        void PrintMessage(string msg)
        {
            Console.WriteLine(msg);
        }
    }
}
```

#### Events
Events are used for signaling between objects. They are based on delegates and provide a way to subscribe to and raise notifications.

**Advantages:**
- **Decoupling:** Decouples event publishers and subscribers.
- **Extensibility:** Allows multiple subscribers for a single event.

**Example:**
```csharp
public class Publisher
{
    public event EventHandler RaiseEvent;

    public void DoSomething()
    {
        OnRaiseEvent(EventArgs.Empty);
    }

    protected virtual void OnRaiseEvent(EventArgs e)
    {
        EventHandler handler = RaiseEvent;
        if (handler != null)
        {
            handler(this, e);
        }
    }
}

public class Subscriber
{
    public void HandleEvent(object sender, EventArgs e)
    {
        Console.WriteLine("Event handled.");
    }
}

class Program
{
    static void Main()
    {
        Publisher pub = new Publisher();
        Subscriber sub = new Subscriber();

        pub.RaiseEvent += sub.HandleEvent;
        pub.DoSomething();
    }
}
```

#### Lambda Expressions
Lambda expressions are anonymous functions that can contain expressions or statements and are used extensively in LINQ queries.

**Advantages:**
- **Conciseness:** Provides a concise way to write anonymous functions.
- **Readability:** Improves readability of code, especially in LINQ queries.

**Example:**
```csharp
Func<int, int, int> add = (x, y) => x + y;
Console.WriteLine(add(2, 3)); // Output: 5

List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };
var evenNumbers = numbers.Where(n => n % 2 == 0).ToList();

evenNumbers.ForEach(n => Console.WriteLine(n)); // Output: 2 4
```

#### Generics
Generics enable type-safe data structures and methods, allowing code reuse and improving performance by eliminating the need for boxing/unboxing.

**Advantages:**
- **Type Safety:** Ensures type safety at compile time.
- **Code Reuse:** Promotes code reuse and reduces redundancy.
- **Performance:** Eliminates the need for boxing/unboxing, improving performance.

**Example:**
```csharp
public class GenericList<T>
{
    private List<T> items = new List<T>();

    public void Add(T item)
    {
        items.Add(item);
    }

    public T Get(int index)
    {
        return items[index];
    }
}

class Program
{
    static void Main()
    {
        GenericList<int> intList = new GenericList<int>();
        intList.Add(1);
        intList.Add(2);

        Console.WriteLine(intList.Get(0)); // Output: 1
        Console.WriteLine(intList.Get(1)); // Output: 2
    }
}
```

#### Extension Methods
Extension methods allow you to add new methods to existing types without modifying their source code or creating new derived types.

**Advantages:**
- **Extensibility:** Adds new methods to existing types without modification.
- **Readability:** Improves readability by allowing method chaining.

**Example:**
```csharp
public static class StringExtensions
{
    public static string Reverse(this string str)
    {
        char[] charArray = str.ToCharArray();
        Array.Reverse(charArray);
        return new string(charArray);
    }
}

class Program
{
    static void Main()
    {
        string example = "Hello";
        Console.WriteLine(example.Reverse()); // Output: olleH
    }
}
```

#### Pattern Matching
Pattern matching simplifies code by allowing you to match data structures and perform actions based on their shape and content.

**Advantages:**
- **Simplicity:** Simplifies complex conditional logic.
- **Readability:** Improves code readability by reducing the need for multiple conditional statements.

**Example:**
```csharp
public static void PrintObjectType(object obj)
{
    switch (obj)
    {
        case int i:
            Console.WriteLine($"Integer: {i}");
            break;
        case string s:
            Console.WriteLine($"String: {s}");
            break;
        case null:
            Console.WriteLine("Null object");
            break;
        default:
            Console.WriteLine("Unknown type");
            break;
    }
}

class Program
{
    static void Main()
    {
        PrintObjectType(5);        // Output: Integer: 5
        PrintObjectType("Hello");  // Output: String: Hello
        PrintObjectType(null);     // Output: Null object
    }
}
```

### Exception Handling
Use try-catch-finally blocks to handle exceptions gracefully. Custom exceptions improve code clarity.

**Advantages:**
- **Robustness:** Improves the robustness of the application by handling runtime errors.
- **Maintainability:** Custom exceptions provide meaningful error messages and improve code maintainability.

**Example:**
```csharp
try
{
    int[] numbers = { 1, 2, 3 };
    Console.WriteLine(numbers[5]);
}
catch (IndexOutOfRangeException ex)
{
    Console.WriteLine($"Error: {ex.Message}");
}
finally
{
    Console.WriteLine("Finally block executed.");
}
```

## Object-Oriented Programming (OOP)

### Encapsulation
Encapsulation involves bundling data and methods operating on the data within a single unit or class. It restricts direct access to some of an object's components.

**Advantages:**
- **Data Protection:** Protects the internal state of objects.
- **Modularity:** Promotes modularity and code organization.

### Abstraction
Abstraction simplifies complex systems by modeling classes appropriate to the problem. It focuses on essential qualities rather than specific characteristics.

**Advantages:**
- **Simplification:** Simplifies complex systems by focusing on essential qualities.
- **Maintenance:** Improves code maintenance by reducing complexity.

### Inheritance
Inheritance allows a class to inherit properties and methods from another class. It promotes code reuse and establishes a relationship between base and derived classes.

**Advantages:**
- **Code Reuse:** Promotes code reuse and reduces redundancy.
- **Hierarchy:** Establishes a hierarchical relationship between classes.

**Example:**
```csharp
public class Animal
{
    public void Eat()
    {
        Console.WriteLine("Eating...");
    }
}

public class Dog : Animal
{
    public void Bark()
    {
        Console.WriteLine("Barking...");
    }
}

class Program
{
    static void Main()
    {
        Dog dog = new Dog();
        dog.Eat(); // Inherited method
        dog.Bark();
    }
}
```

### Polymorphism
Polymorphism enables objects to be treated as instances of their parent class. It allows methods to be overridden in derived classes to provide specific behavior.

**Advantages:**
- **Flexibility:** Provides flexibility by allowing methods to be overridden.
- **Extensibility:** Enhances code extensibility by enabling new behavior without modifying existing code.

**Example:**
```csharp
public class Animal
{
    public virtual void Speak()
    {
        Console.WriteLine("Animal sound");
    }
}

public class Dog : Animal
{
    public override void Speak()
    {
        Console.WriteLine("Bark");
    }
}

class Program
{
    static void Main()
    {
        Animal myDog = new Dog();
        myDog.Speak(); // Output: Bark
    }
}
```

## SOLID Principles & Design Patterns

### SOLID Principles
- **Single Responsibility Principle**: A class should have only one reason to change.
- **Open/Closed Principle**: Software entities should be open for extension but closed for modification.
- **Liskov Substitution Principle**: Derived classes should be substitutable for their base classes.
- **Interface Segregation Principle**: Clients should not be forced to depend on interfaces they do not use.
- **Dependency Inversion Principle**: Depend on abstractions, not concretions.

#### Single Responsibility Principle
A class should have only one reason to change, meaning it should only have one job or responsibility.

**Advantages:**
- **Maintainability:** Improves maintainability by reducing the complexity of classes.
- **Testability:** Enhances testability by isolating class responsibilities.

**Example:**
```csharp
public class Invoice
{
    public void CalculateTotal() { /* ... */ }
}

public class InvoicePrinter
{
    public void Print(Invoice invoice) { /* ... */ }
}

public class InvoiceSaver
{
    public void Save(Invoice invoice) { /* ... */ }
}
```

#### Open/Closed Principle
Software entities should be open for extension but closed for modification. You can extend the behavior of a class without modifying its source code.

**Advantages:**
- **Extensibility:** Enhances extensibility by allowing new functionality to be added without modifying existing code.
- **Stability:** Improves stability by reducing the risk of introducing bugs in existing code.

**Example:**
```csharp
public abstract class Shape
{
    public abstract double Area();
}

public class Circle : Shape
{
    public double Radius { get; set; }

    public override double Area()
    {
        return Math.PI * Radius * Radius;
    }
}

public class Rectangle : Shape
{
    public double Width { get; set; }
    public double Height { get; set; }

    public override double Area()
    {
        return Width * Height;
    }
}
```

#### Liskov Substitution Principle
Derived classes should be substitutable for their base classes without altering the correctness of the program.

**Advantages:**
- **Reliability:** Ensures that derived classes can be used interchangeably with base classes without affecting the correctness of the program.
- **Consistency:** Promotes consistency and predictability in code behavior.

**Example:**
```csharp
public class Bird
{
    public virtual void Fly() { /* ... */ }
}

public class Eagle : Bird
{
    public override void Fly() { /* ... */ }
}

public class Ostrich : Bird
{
    public override void Fly()
    {
        throw new InvalidOperationException("Ostriches can't fly");
    }
}
```

#### Interface Segregation Principle
Clients should not be forced to depend on interfaces they do not use. Split large interfaces into smaller, more specific ones.

**Advantages:**
- **Decoupling:** Reduces coupling between classes by providing more specific interfaces.
- **Flexibility:** Enhances flexibility by allowing classes to implement only the interfaces they need.

**Example:**
```csharp
public interface IPrinter
{
    void PrintDocument();
}

public interface IScanner
{
    void ScanDocument();
}

public class MultiFunctionPrinter : IPrinter, IScanner
{
    public void PrintDocument() { /* ... */ }
    public void ScanDocument() { /* ... */ }
}

public class SimplePrinter : IPrinter
{
    public void PrintDocument() { /* ... */ }
}
```

#### Dependency Inversion Principle
Depend on abstractions, not concretions. High-level modules should not depend on low-level modules.

**Advantages:**
- **Flexibility:** Enhances flexibility by allowing high-level modules to depend on abstractions rather than concrete implementations.
- **Testability:** Improves testability by enabling dependency injection.

**Example:**
```csharp
public interface ILogger
{
    void Log(string message);
}

public class ConsoleLogger : ILogger
{
    public void Log(string message)
    {
        Console.WriteLine(message);
    }
}

public class FileLogger : ILogger
{
    public void Log(string message)
    {
        // Write log to file
    }
}

public class UserService
{
    private readonly ILogger _logger;

    public UserService(ILogger logger)
    {
        _logger = logger;
    }

    public void CreateUser(string username)
    {
        // Create user
        _logger.Log("User created: " + username);
    }
}
```

### Design Patterns
- **Singleton**: Ensures a class has only one instance and provides a global point of access.
- **Factory**: Creates objects without specifying the exact class of the object that will be created.
- **Observer**: Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified.
- **Strategy**: Defines a family of algorithms, encapsulates each one, and makes them interchangeable.

#### Singleton Pattern
Ensures a class has only one instance and provides a global point of access.

**Advantages:**
- **Controlled Access:** Provides controlled access to the single instance.
- **Resource Management:** Ensures that only one instance of the class is created, reducing resource consumption.

**Example:**
```csharp
public class Singleton
{
    private static Singleton _instance;

    private Singleton() { }

    public static Singleton Instance
    {
        get
        {
            if (_instance == null)
            {
                _instance = new Singleton();
            }
            return _instance;
        }
    }
}
```

#### Factory Pattern
Creates objects without specifying the exact class of the object that will be created.

**Advantages:**
- **Decoupling:** Decouples the client code from the object creation process.
- **Extensibility:** Allows easy addition of new types without modifying existing code.

**Example:**
```csharp
public interface IProduct
{
    void DoSomething();
}

public class ConcreteProductA : IProduct
{
    public void DoSomething()
    {
        Console.WriteLine("Product A");
    }
}

public class ConcreteProductB : IProduct
{
    public void DoSomething()
    {
        Console.WriteLine("Product B");
    }
}

public class ProductFactory
{
    public IProduct CreateProduct(string type)
    {
        switch (type)
        {
            case "A": return new ConcreteProductA();
            case "B": return new ConcreteProductB();
            default: throw new ArgumentException("Invalid type");
        }
    }
}
```

#### Observer Pattern
Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified.

**Advantages:**
- **Decoupling:** Decouples the subject from its observers.
- **Scalability:** Allows multiple observers to be notified of state changes.

**Example:**
```csharp
public interface IObserver
{
    void Update();
}

public class ConcreteObserver : IObserver
{
    public void Update()
    {
        Console.WriteLine("Observer notified");
    }
}

public class Subject
{
    private List<IObserver> observers = new List<IObserver>();

    public void Attach(IObserver observer)
    {
        observers.Add(observer);
    }

    public void Detach(IObserver observer)
    {
        observers.Remove(observer);
    }

    public void Notify()
    {
        foreach (var observer in observers)
        {
            observer.Update();
        }
    }
}
```

#### Strategy Pattern
Defines a family of algorithms, encapsulates each one, and makes them interchangeable.

**Advantages:**
- **Flexibility:** Allows algorithms to be selected at runtime.
- **Extensibility:** Enables easy addition of new algorithms without modifying existing code.

**Example:**
```csharp
public interface IStrategy
{
    void Execute();
}

public class