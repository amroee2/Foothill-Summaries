# OOP

Object-Oriented Programming (OOP) in C# is a paradigm that uses "objects" to design software. It allows for the creation of classes that define properties, methods, and events to model real-world entities.

# Classes and Objects

- Classes: they represent the blueprint for an object, they contain all the members that each object have.
- Objects: they are "instances" of classes, they are used to model the program into a real world application.

## Classes

Classes are defined using the access modifier then the name of the class.

![image](https://github.com/user-attachments/assets/2773e656-8cb3-42dc-858c-d96247e58c02)

A top level or outer class can only be public or internal, nested classes can have any of the 5 access modifiers.

**The members that classes contain:**

## Properties and fields

 - Fields: they are variables that are declared directly in a class. They store data and are typically used for internal class implementation.

![image](https://github.com/user-attachments/assets/7432881b-b7b8-480a-af0c-2a4e2844e6a9)

 - Properties: Properties are members that provide a flexible mechanism to read, write, or compute the value of a private field. They are used to encapsulate the fields of a class and add control over how the data is accessed or modified.
 - 
![image](https://github.com/user-attachments/assets/0493d6ac-eda7-4c2a-a003-879e57be8ab7)

**Properties in C# are like fields but with built-in getters and setters that allow you to control how the field is accessed and modified.**

## Methods

Methods in C# are blocks of code that perform specific tasks and can be called upon when needed. They are used to define the behavior of a class and can accept input (parameters), perform operations, and return results.

![image](https://github.com/user-attachments/assets/fc2838eb-6f48-45a4-b5df-743f219c8898)

## Objects

As mentioned before objects are instances of a class, they contain everything that has been initialized in the said class.

An instance can be defined through a **constructor**, which can be either empty or contain some/all of the arguments, and then called to instaniate an object.

A class can have multiple constructors, and the compiler knows which one depending on the number of parameters passed, datatype and the order, in what is known as **overloading**

**this** refers to the current instance using the constructor.
![image](https://github.com/user-attachments/assets/1ee0447c-0d9a-461c-a8d5-102bad9b00c5)
![image](https://github.com/user-attachments/assets/91e308bd-3582-442b-95c9-7d7b52431146)

## Static keyword

Static members of a class are members that can only be called/accessed by the class itself, not by the instances of the class.

In here for example, we only have one inventory, we dont want each instaance of the class to have an inventory of its own, so we declare it as static.
![image](https://github.com/user-attachments/assets/adf63f8f-de12-4cf5-935b-51d70ae63093)

There can be static methods as well, and they also can only be called by the class itself, **and can only contain static members of the class**, that applies to both methods and properties. 

# Object-Oriented Programming (OOP) is centered around four main principles: Encapsulation, Inheritance, Polymorphism, and Abstraction. 

## Encapsulation

Encapsulation is the concept of bundling the data (fields) and the methods that operate on the data into a single unit or class, and restricting access to some of the object's components.

```
public class Account
{
    private decimal balance; // Private field

    public void Deposit(decimal amount) // Public method
    {
        if (amount > 0)
        {
            balance += amount;
        }
    }

    public decimal GetBalance() // Public method
    {
        return balance;
    }
}
```

Can also be done through properties 

```
 private decimal balance;

    // Encapsulated through a property
    public decimal Balance
    {
        get { return balance; } // Provides controlled access
        private set // Restricts modification to within the class
        {
            if (value >= 0)
            {
                balance = value;
            }
        }
    }
```
## Inheritance 

Inheritance allows a new class (derived class) to inherit the fields and methods of an existing class (base class).

Its used to avoid code repetition and make it more readable whilst also drawing the relationships between classes, base class can also **inherit** data members from the base class depending on their access modifier 
```
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
```
## Polymorphism

Polymorphism allows methods to do different things based on the object it is acting upon. There are two types: compile-time (method overloading) and run-time (method overriding).

### Overriding

```
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

public class Cat : Animal
{
    public override void Speak()
    {
        Console.WriteLine("Meow");
    }
}
```
When Speak is called on an object of type Animal, the method corresponding to the actual object type (e.g., Dog or Cat) is invoked at runtime.

```
Animal myAnimal = new Dog();
myAnimal.Speak() //Bark;
Animal myAnimal = new Cat();
myAnimal.Speak() //Meow;

```
- virtual: Used in the base class to indicate that a method can be overridden.
- override: Used in the derived class to provide a new implementation for an inherited method.

**Method hiding**

If we omit the polymorphism operation but we want to give a derived class and a base class the same method name, we use the **new** keyword, so base class calls its method and derived ones call their own, in what is known as method hiding.

```
public class BaseClass
{
    public void Show()
    {
        Console.WriteLine("BaseClass Show");
    }
}

public class DerivedClass : BaseClass
{
    public new void Show()
    {
        Console.WriteLine("DerivedClass Show");
    }
}

BaseClass baseObj = new BaseClass();
BaseClass derivedAsBase = new DerivedClass();
DerivedClass derivedObj = new DerivedClass();

baseObj.Show();           // Output: BaseClass Show
derivedAsBase.Show();    // Output: BaseClass Show (method in base class is called)
derivedObj.Show();       // Output: DerivedClass Show (method in derived class is called)
```
## Method overloading

When two methods share the same name, but they either differ in 

1. return type
2. Number of parameters and their datatype
3. order of parameters

```
public class MathOperations
{
    public int Add(int a, int b)
    {
        return a + b;
    }

    public double Add(double a, double b)
    {
        return a + b;
    }
}
```

As mentioned before, we can also have constructors overloading as well.

## Abstraction

Abstraction is the concept of hiding the complex implementation details and showing only the essential features of an object.

## Abstract classes

An abstract class is a class that cannot be instantiated on its own and is meant to be inherited. It can contain both abstract members (methods, properties, etc.) that must be implemented by derived classes and concrete members that have implementation.

Features of Abstract Classes:

- Abstract Members: Can define methods, properties, or events without any implementation, which derived classes must implement.
- Concrete Members: Can also include methods and properties with complete implementations.
- Inheritance: A class can inherit only one abstract class (C# supports single inheritance for classes).
- Fields: Can include fields (variables) with data, which can be used by the derived classes.
- Access Modifiers: Abstract classes can have different access modifiers (e.g., public, protected, etc.) for their members.
- Constructors: Can have constructors, which can be called from derived classes to initialize shared fields.
```
public abstract class Shape
{
    public abstract double GetArea();
}

public class Circle : Shape
{
    public double Radius { get; set; }

    public Circle(double radius)
    {
        Radius = radius;
    }

    public override double GetArea()
    {
        return Math.PI * Radius * Radius;
    }
}
```
## Interfaces

An interface defines a contract that a class or struct must adhere to. It only contains the signatures of methods, properties, events, or indexers, without any implementation (before C# 8.0). From C# 8.0 onward, interfaces can include default implementations.

Features of Interfaces:
- Only Declarations: Only method, property, event, or indexer declarations (signatures); no fields or constructors.
- Multiple Inheritance: A class or struct can implement multiple interfaces.
- No Fields: Unlike java, Interfaces cannot have data fields; all members must be public .
- Default Implementations (C# 8.0+): Starting from C# 8.0, interfaces can provide default method implementations.
- Implicit Implementation: Classes that implement interfaces must provide the required functionality for all members of the interface.

```
public interface IAnimal
{
    void MakeSound();
}

public class Cat : IAnimal
{
    // Must implement the interface method
    public void MakeSound()
    {
        Console.WriteLine("Meow");
    }
}

```

In C#, there are several predefined interfaces in the .NET framework that provide common functionality to classes. One such example is the ICloneable interface, which allows for creating a copy of an object.

```
public class Person : ICloneable
{
    public string Name { get; set; }
    public int Age { get; set; }

    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }

    // Implementing the Clone method from ICloneable
    public object Clone()
    {
        return new Person(Name, Age); // Returns a shallow copy of the object
    }
}
```

- Shallow Copy: Copies the object's fields as-is, but if a field is a reference type, it points to the same memory location.
- Deep Copy: Copies the object and recursively copies all objects it references, so all objects are independent.
## Sealed Keyword

Sealed keyword is used to indicate whether a class can no longer be extended (prevents further inheritance), and on a method to prevent it from being overridden.

```
public sealed class SealedClass
{
    // This class can't be inherited
}

public class BaseClass
{
    public virtual void Display() { }
}

public class DerivedClass : BaseClass
{
    public sealed override void Display()
    {
        // This method can't be overridden further
    }
}
```

## Partial classes

Partial classes are just a simple way to make the class members be more readable. In large programs, a class can have a lot of members (methods, events, data variables) which can make the class very big, one way to get behind this is through partial classes, which basically allow you to seperate a class intwo 2 files.

```
// File 1
public partial class MyClass
{
    public void Method1() { }
}

// File 2
public partial class MyClass
{
    public void Method2() { }
}

```
## Constructor chaining

we already mentioned that a class can have multiple constructors, and that we can utilize the **this** keyword in a class to refer to the current object instance, we can also use this to **chain** constructors (call one from the other).

```
public class Person
{
    public string Name { get; set; }

    public Person() : this("Unknown") { } // Calls the other constructor

    public Person(string name)
    {
        Name = name;
    }
}
```
## Exception handling

Exception handling in C# allows developers to manage runtime errors gracefully without crashing the program. It uses the try, catch, finally, and throw keywords to handle exceptions and recover from them.

- try-catch block: try contains the code that might cause the exception, the catch block is responsible of "catching it" and handling it.
```
try
{
    int result = 10 / 0; // This will throw a DivideByZeroException
}
catch (DivideByZeroException ex)
{
    Console.WriteLine("Cannot divide by zero!");
}
```
we can have multiple catch blocks for the same try block

- Finally block: The finally block contains code that always runs, regardless of whether an exception was thrown or caught. It’s typically used to release resources like file handles, database connections, etc.

```
try
{
    // Code that may throw an exception
}
catch (Exception ex)
{
    Console.WriteLine("An error occurred.");
}
finally
{
    Console.WriteLine("This block always runs.");
}
```
- throw: The throw keyword is used to manually throw an exception. It can be used to signal that an exceptional situation has occurred.

```
public void Divide(int a, int b)
{
    if (b == 0)
        throw new DivideByZeroException("Denominator cannot be zero.");
    
    Console.WriteLine(a / b);
}
```

- Compile-Time Exceptions: These are caught by the compiler, such as syntax errors or invalid data types. These errors prevent the program from compiling and must be fixed before running the program.
- Run-Time Exceptions: These occur during the execution of a program, such as dividing by zero, accessing a null object, or invalid array indexing. These are caught using the try-catch mechanism.
