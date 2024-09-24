# Decorator

The Decorator design pattern is a structural pattern used to extend the behavior of objects dynamically by "wrapping" them in other objects. It allows adding functionalities to individual objects, rather than to a whole class, without modifying the class itself. The pattern helps in adhering to the Open/Closed Principle (OCP), as the core functionality is kept intact while allowing the addition of new behaviors.

Key Concepts

- Component: Defines an interface for objects that can have responsibilities added to them dynamically.
- ConcreteComponent: The object to which additional functionalities will be added.
- Decorator: An abstract class that implements the Component interface and contains a reference to a Component object.
- ConcreteDecorator: The class that extends Decorator to add new behaviors.

```csharp
// Component Interface
public interface ICoffee
{
    string GetDescription();
    double GetCost();
}

// ConcreteComponent
public class Espresso : ICoffee
{
    public string GetDescription() => "Espresso";
    public double GetCost() => 2.0;
}

// ConcreteComponent
public class Latte : ICoffee
{
    public string GetDescription() => "Latte";
    public double GetCost() => 3.5;
}

// Base Decorator
public abstract class CoffeeDecorator : ICoffee
{
    protected ICoffee _coffee;
    
    public CoffeeDecorator(ICoffee coffee)
    {
        _coffee = coffee;
    }

    public virtual string GetDescription() => _coffee.GetDescription();
    public virtual double GetCost() => _coffee.GetCost();
}

// ConcreteDecorator 1: Add Milk
public class MilkDecorator : CoffeeDecorator
{
    public MilkDecorator(ICoffee coffee) : base(coffee) { }

    public override string GetDescription() => _coffee.GetDescription() + ", Milk";
    public override double GetCost() => _coffee.GetCost() + 0.5;
}

// ConcreteDecorator 2: Add Sugar
public class SugarDecorator : CoffeeDecorator
{
    public SugarDecorator(ICoffee coffee) : base(coffee) { }

    public override string GetDescription() => _coffee.GetDescription() + ", Sugar";
    public override double GetCost() => _coffee.GetCost() + 0.2;
}

// ConcreteDecorator 3: Add Caramel
public class CaramelDecorator : CoffeeDecorator
{
    public CaramelDecorator(ICoffee coffee) : base(coffee) { }

    public override string GetDescription() => _coffee.GetDescription() + ", Caramel";
    public override double GetCost() => _coffee.GetCost() + 0.7;
}

// Usage Example
class Program
{
    static void Main(string[] args)
    {
        ICoffee myCoffee = new Espresso();
        Console.WriteLine($"{myCoffee.GetDescription()} costs {myCoffee.GetCost()}");

        // Add Milk
        myCoffee = new MilkDecorator(myCoffee);
        Console.WriteLine($"{myCoffee.GetDescription()} costs {myCoffee.GetCost()}");

        // Add Sugar
        myCoffee = new SugarDecorator(myCoffee);
        Console.WriteLine($"{myCoffee.GetDescription()} costs {myCoffee.GetCost()}");

        // Add Caramel
        myCoffee = new CaramelDecorator(myCoffee);
        Console.WriteLine($"{myCoffee.GetDescription()} costs {myCoffee.GetCost()}");
    }
}
```

Use Cases:

- Adding Responsibilities: If you need to add responsibilities or behaviors dynamically (like adding features to coffee in the example), Decorator is useful.
- When Inheritance is Not Feasible: When extending functionalities using inheritance leads to a large number of subclasses or bloated class hierarchies.
- Flexible Configuration: The pattern allows for configuring classes at runtime by decorating them with different combinations of features.

Advantages:

- Single Responsibility Principle: Decorators allow behavior to be divided into different classes, keeping each class focused on a single responsibility.
- Open/Closed Principle: Existing classes don’t need to be modified when adding new behaviors.
- Flexible Behavior Addition: You can mix and match decorators to create unique combinations of functionality.
- Avoids Class Explosion: By using composition over inheritance, you avoid creating too many subclasses to cover all combinations of features.

Disadvantages:

- Complexity: The decorator pattern can add a layer of complexity with too many small objects when there are many decorators involved.
- Order-Dependent: The order in which decorators are applied can affect the resulting behavior, which can be confusing if not managed properly.
- Difficult Debugging: Tracing issues can become difficult when multiple layers of decorators are used.
