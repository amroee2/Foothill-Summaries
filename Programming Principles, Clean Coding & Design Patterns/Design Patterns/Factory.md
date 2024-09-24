# Factory 

In C#, the Factory Design Pattern is a creational pattern that provides a way to create objects without specifying the exact class of object that will be created. There are three main types of factory patterns:

- Simple Factory
- Factory Method
- Abstract Factory

## Simple Factory

A class with a static method that decides which subclass or class to instantiate. It's not a true design pattern but a programming idiom.

```csharp
public class Pizza
{
    public string Name { get; set; }
}

public class CheesePizza : Pizza
{
    public CheesePizza() => Name = "Cheese Pizza";
}

public class PepperoniPizza : Pizza
{
    public PepperoniPizza() => Name = "Pepperoni Pizza";
}

public class PizzaFactory
{
    public static Pizza CreatePizza(string type)
    {
        return type switch
        {
            "Cheese" => new CheesePizza(),
            "Pepperoni" => new PepperoniPizza(),
            _ => throw new ArgumentException("Invalid pizza type")
        };
    }
}
```

Use Cases:

- When the creation logic is simple and doesn't need an interface for creating objects.
- To encapsulate object creation logic within a single class.

Advantages:

- Centralizes the creation logic.
- Makes it easy to manage object creation.

Disadvantages:

- Violates the Open/Closed Principle (OCP) as adding new types requires modifying the factory method.
- Not as flexible as other factory patterns.

## Factory Method

Defines an interface for creating an object, but lets subclasses decide which class to instantiate. It lets a class defer instantiation to subclasses.

```csharp
public abstract class Pizza
{
    public string Name { get; set; }
    public abstract void Prepare();
}

public class CheesePizza : Pizza
{
    public CheesePizza() => Name = "Cheese Pizza";
    public override void Prepare() => Console.WriteLine("Preparing Cheese Pizza");
}

public class PepperoniPizza : Pizza
{
    public PepperoniPizza() => Name = "Pepperoni Pizza";
    public override void Prepare() => Console.WriteLine("Preparing Pepperoni Pizza");
}

public abstract class PizzaStore
{
    public Pizza OrderPizza(string type)
    {
        Pizza pizza = CreatePizza(type);
        pizza.Prepare();
        return pizza;
    }
    
    protected abstract Pizza CreatePizza(string type);
}

public class NYPizzaStore : PizzaStore
{
    protected override Pizza CreatePizza(string type)
    {
        return type switch
        {
            "Cheese" => new CheesePizza(),
            "Pepperoni" => new PepperoniPizza(),
            _ => throw new ArgumentException("Invalid pizza type")
        };
    }
}
```

Use Cases:

- When a class can't anticipate the class of objects it must create.
- To delegate responsibility for creation to subclasses.

Advantages:

- Adheres to the Single Responsibility Principle (SRP).

Disadvantages:

- Can introduce a lot of classes into the system.
- Increases the complexity of the code.

## Abstract Factory

Provides an interface for creating families of related or dependent objects without specifying their concrete classes.

```csharp
// Abstract Product
public interface IDough { }
public interface ISauce { }

// Concrete Products
public class ThickCrustDough : IDough { }
public class MarinaraSauce : ISauce { }
public class ThinCrustDough : IDough { }
public class PlumTomatoSauce : ISauce { }

// Abstract Factory
public interface IPizzaIngredientFactory
{
    IDough CreateDough();
    ISauce CreateSauce();
}

// Concrete Factories
public class NYPizzaIngredientFactory : IPizzaIngredientFactory
{
    public IDough CreateDough() => new ThinCrustDough();
    public ISauce CreateSauce() => new MarinaraSauce();
}

public class ChicagoPizzaIngredientFactory : IPizzaIngredientFactory
{
    public IDough CreateDough() => new ThickCrustDough();
    public ISauce CreateSauce() => new PlumTomatoSauce();
}

// Client
public abstract class Pizza
{
    protected string Name;
    protected IDough Dough;
    protected ISauce Sauce;
    protected abstract void Prepare();
}

public class CheesePizza : Pizza
{
    private readonly IPizzaIngredientFactory _ingredientFactory;

    public CheesePizza(IPizzaIngredientFactory ingredientFactory)
    {
        _ingredientFactory = ingredientFactory;
    }

    protected override void Prepare()
    {
        Console.WriteLine("Preparing " + Name);
        Dough = _ingredientFactory.CreateDough();
        Sauce = _ingredientFactory.CreateSauce();
    }
}
```

Use Cases:

- When a system needs to be independent of how its products are created.
- To enforce constraints regarding which objects can be used together.

Advantages:

- Ensures that related objects are used together.

Disadvantages:

- Can be challenging to add new products because changes are required across multiple classes.
- The complexity increases with the number of product families.
