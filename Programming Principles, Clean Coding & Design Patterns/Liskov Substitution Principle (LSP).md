# Liskov Substitution Principle (LSP)

Objects of a derived class must be substitutable for objects of the base class without altering the correctness of the program.

In simpler terms, this means that if class B is a subclass of class A, then anywhere A is expected, B should be able to replace it without causing issues in the program’s functionality.

Key Points of LSP:

- Subtypes must behave like their parent types: Subclasses should adhere to the behavior expected from the base class. If they don’t, they violate LSP.
- Avoid unexpected behavior: A subclass should not override base class methods in a way that changes their behavior (e.g., breaking contract).
- Ensure consistent functionality: Any change in the subclass should enhance or extend the base class's functionality, not contradict it.

Why LSP is Important:

- Predictable Substitution: When you replace an instance of a class with its subclass, everything should work seamlessly without unexpected results.
- Inheritance and Polymorphism: LSP ensures that you can use polymorphism safely, relying on the base class’s behavior and contracts.
- Reduces Errors: Violating LSP can lead to bugs, especially when subclasses behave in ways that are inconsistent with the base class.

Example

Here, the subclass Penguin violates the LSP. Even though it is a bird, it cannot fly. If we substitute Penguin in a place where a Bird is expected and call Fly(), it will break the program by throwing an exception, which violates the LSP. The client code will expect all Bird objects to be able to fly, but Penguin does not behave as a bird that can fly.

```csharp
public class Bird
{
    public virtual void Fly()
    {
        Console.WriteLine("I can fly!");
    }
}

public class Penguin : Bird
{
    public override void Fly()
    {
        throw new NotSupportedException("Penguins can't fly!");
    }
}
```

One solution can be done is through inheritance:

```csharp
public class Bird
{
    public virtual void Move()
    {
        Console.WriteLine("I am moving!");
    }
}

public class FlyingBird : Bird
{
    public override void Move()
    {
        Console.WriteLine("I am flying!");
    }
}

public class Penguin : Bird
{
    public override void Move()
    {
        Console.WriteLine("I am swimming!");
    }
}
```

Or interfaces

```csharp
// General bird interface, common to all birds
public interface IBird
{
    void Eat();
    void Move();
}

// Interface for birds that can fly
public interface IFlyable
{
    void Fly();
}

// A class for birds that can fly
public class Eagle : IBird, IFlyable
{
    public void Eat()
    {
        Console.WriteLine("Eagle is eating.");
    }

    public void Move()
    {
        Console.WriteLine("Eagle is walking.");
    }

    public void Fly()
    {
        Console.WriteLine("Eagle is flying.");
    }
}

// A class for birds that cannot fly
public class Penguin : IBird
{
    public void Eat()
    {
        Console.WriteLine("Penguin is eating.");
    }

    public void Move()
    {
        Console.WriteLine("Penguin is swimming.");
    }
}
```
