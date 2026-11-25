| Feature | `interface` | `abstract class` |
|---|---|---|
| Purpose | Defines a contract (what a type can do) | Defines a base type with shared state/behavior (what a type is) |
| Inheritance | A class can implement **multiple** interfaces | A class can inherit **only one** abstract class |
| Fields | Not allowed (instance fields) | Allowed |
| Constructors | Not allowed | Allowed |
| Method implementation | Optional (default interface methods, C# 8+) | Allowed (regular and abstract methods) |
| Access modifiers | Members public by default (private/protected allowed with default implementations) | Any modifier (`private`, `protected`, `public`, etc.) |
| Instantiation | Cannot be instantiated | Cannot be instantiated |
| Properties / events / indexers | Yes | Yes |
| Static members | Yes (C# 8+, including static abstract in C# 11) | Yes |
| Naming convention | Starts with `I` (`IRepository`) | No special convention |

#### Interface example

```csharp
public interface INotifier
{
    void Send(string message);
}

public class EmailNotifier : INotifier
{
    public void Send(string message) => Console.WriteLine($"Email: {message}");
}

public class SmsNotifier : INotifier
{
    public void Send(string message) => Console.WriteLine($"SMS: {message}");
}
```

A class can implement several interfaces:

```csharp
public class Logger : ILogger, IDisposable { ... }
```

#### Abstract class example

```csharp
public abstract class Device
{
    public string Name { get; set; }

    protected Device(string name) => Name = name;

    // Shared implementation
    public void PowerOn() => Console.WriteLine($"{Name} is on");

    // Must be implemented by derived classes
    public abstract void Run();

    // Can optionally be overridden
    public virtual void Reset() => Console.WriteLine("Resetting...");
}

public class Printer : Device
{
    public Printer() : base("Printer") { }

    public override void Run() => Console.WriteLine("Printing...");
}
```

#### Default interface methods (C# 8+)

```csharp
public interface ILogger
{
    void Log(string message);

    void LogError(string message) => Log($"ERROR: {message}"); // default implementation
}
```

#### When to use which

| Situation | Choose |
|---|---|
| Unrelated classes need the same capability (e.g., `IDisposable`, `IComparable`) | Interface |
| You need multiple inheritance of behavior contracts | Interface |
| Dependency injection, mocking, unit testing | Interface |
| Related classes share common code, fields, or constructor logic | Abstract class |
| You want to provide a partial implementation and force subclasses to complete it | Abstract class |
| You need `protected` members or state shared across the hierarchy | Abstract class |

#### Using them together

A common pattern is to expose an interface and provide an abstract base class with shared logic:

```csharp
public interface IPaymentProcessor
{
    void Process(decimal amount);
}

public abstract class PaymentProcessorBase : IPaymentProcessor
{
    public void Process(decimal amount)
    {
        Validate(amount);
        Execute(amount);
    }

    protected virtual void Validate(decimal amount)
    {
        if (amount <= 0) throw new ArgumentException("Invalid amount");
    }

    protected abstract void Execute(decimal amount);
}

public class StripeProcessor : PaymentProcessorBase
{
    protected override void Execute(decimal amount) => Console.WriteLine($"Stripe: {amount}");
}
```

#### Rule of thumb

- **Interface** = "can do" (capability, contract).
- **Abstract class** = "is a" (shared identity, common implementation).
