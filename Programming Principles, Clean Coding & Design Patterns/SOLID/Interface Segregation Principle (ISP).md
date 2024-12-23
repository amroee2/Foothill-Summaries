# Interface Segregation Principle

The Interface Segregation Principle (ISP) is one of the SOLID principles in object-oriented design. It suggests that no client should be forced to implement methods it does not use. Instead of having one large interface with multiple methods, it is better to divide it into smaller, more specific interfaces, allowing clients to depend only on the functionalities they actually need.

Example

```csharp

// Before ISP
public interface IWorker
{
    void Work();              // Regular work
    void ManageTeam();        // Management work
}

public class Developer : IWorker
{
    public void Work() 
    {
        Console.WriteLine("Coding...");
    }

    // Developers don't manage teams, but they are forced to implement this
    public void ManageTeam() 
    {
        throw new NotImplementedException();
    }
}

public class Manager : IWorker
{
    public void Work()
    {
        Console.WriteLine("Managing projects...");
    }

    public void ManageTeam()
    {
        Console.WriteLine("Managing team...");
    }
}
```

Apply ISP

```csharp

// After ISP
public interface IWorker
{
    void Work();  // Regular work
}

public interface IManager
{
    void ManageTeam();  // Management work
}

public class Developer : IWorker
{
    public void Work() 
    {
        Console.WriteLine("Coding...");
    }
    // Now, Developer doesn't need to implement ManageTeam()
}

public class Manager : IWorker, IManager
{
    public void Work() 
    {
        Console.WriteLine("Managing projects...");
    }

    public void ManageTeam() 
    {
        Console.WriteLine("Managing team...");
    }
}
```

Benefits of Interface Segregation Principle:

- Code Flexibility: Classes implement only the methods they need, making them easier to maintain.
- Reusability: Small interfaces are more reusable, as they target specific roles or behaviors.
- Avoid Unnecessary Dependencies: Clients are not forced to depend on or implement methods that they do not need.
- Reduces the Impact of Changes: Since classes implement only what they use, changes in one part of the system (such as adding new methods to interfaces) won’t unnecessarily affect other parts.
