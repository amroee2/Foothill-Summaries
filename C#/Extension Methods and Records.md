# Extension methods

Extension methods in C# are a powerful feature that allows you to add new methods to existing types without modifying the original type, inheriting from it, or recompiling the source code. 

## How to use extension methods

Assume this product class

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ExtensionMethods
{
    public class Product
    {
        public string Name { get; set; }
        public decimal Price { get; set; }

        public Product(string name, decimal price)
        {
            Name = name;
            Price = price;
        }
    }
}
```

We can add a simple extension method by doing this

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ExtensionMethods
{
    public static class ProductExtensions
    {
        public static string ToFormattedString(this Product product)
        {
            return string.Format("{0}: {1} From extenstion", product.Name, product.Price);
        }
    }
}
```

- Static class: The class must be static as extension methods are not meant to be tied into one instance
- This in parameter list: The this keyword in the method signature is what makes a static method an extension method. It tells the C# compiler that this method is intended to be used as an extension method for the type specified after this.

# Extension methods hiding

Extension methods can be **hidden** if there is a similar method in the targeted class.

In program.cs

```
using ExtensionMethods;

Product product = new Product("Widget", 9.99m);
Console.WriteLine(product.ToFormattedString());
```

This would output

![image](https://github.com/user-attachments/assets/e867640d-d0d4-4a0f-b010-c2a99891b262)

But if we update the product class

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ExtensionMethods
{
    public class Product
    {
        public string Name { get; set; }
        public decimal Price { get; set; }

        public Product(string name, decimal price)
        {
            Name = name;
            Price = price;
        }
        public string ToFormattedString()
        {
            return string.Format("{0}: {1} From product class", Name, Price);
        }
    }
}
```

This would output this

![image](https://github.com/user-attachments/assets/5f7cddef-fe6a-41ce-a5ae-07d74feec772)


# Records

In C#, records are a special type of reference types, They provide a concise syntax for creating immutable data objects.

They are essentially fancy classes with additional features.

## Classes vs Records

Remember our product class

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ExtensionMethods
{
    public class Product
    {
        public string Name { get; set; }
        public decimal Price { get; set; }

        public Product(string name, decimal price)
        {
            Name = name;
            Price = price;
        }
        public string ToFormattedString()
        {
            return string.Format("{0}: {1} From product class", Name, Price);
        }
    }
}
```

this is how a record is created

```
public record Record1(string Name, int Price);
```

Records are immutable, which means after we initialize a record instance it cant be changed, rather it will just create a new reference type in memory, Classes can be closer to records if we replace **set** with **init** in properties.

A record and a class can be instaniated the same way:

```
var record1 = new Record1("Candy", 10);
Product product = new("Candy", 10);
```

## ToString implementation

When printing a class using Console.WriteLine, we only get the name of it:

![image](https://github.com/user-attachments/assets/2cd0e141-7219-4a91-b593-eebb8f7dbc41)

While for records, it prints the information of its properties:

![image](https://github.com/user-attachments/assets/660e18e0-7766-4a3e-904e-a223843687ec)

## Equals and Reference Equals

Assume we have these instances

```
var record1 = new Record1("Candy", 10);
var record2 = new Record1("Candy", 10);
var record3 = new Record1("Candy", 20);
Product product1 = new("Candy", 10);
Product product2 = new("Candy", 10);
Product product3 = new("Candy", 20);
```

We can compare records using Equals method, it will compare the actual values of the properties, not the reference types.

```
Console.WriteLine(record1 == record2); //True
Console.WriteLine(record1 == record3); //False
```

Whilst for classes, it will compare the refernce value

```
Console.WriteLine(product1 == product2); //Flase
Console.WriteLine(product1 == product3); //False
```

Note that Equals and == serve different purposes, but if Equals is **not overridden**, it will act the same as ==

We can compare references using reference equals:

```
Console.WriteLine(ReferenceEquals(record1,record2)); //False
```

## GetHashCode
```
Console.WriteLine(record1.GetHashCode());
Console.WriteLine(record2.GetHashCode());
Console.WriteLine(record3.GetHashCode());
Console.WriteLine(product1.GetHashCode());
Console.WriteLine(product2.GetHashCode());
Console.WriteLine(product3.GetHashCode());
```

Output:

```
89797639
89797639
89797649
18643596
33574638
33736294
```

Notice that the first 2 records shared the same Hash code.

# Deconstructor

We can access the values within a record using deconstructor:

```
var (name, price) = record1;

Console.WriteLine($"{name}, {price}");

```

in classes, this would need a new method we can pass the arguments to and set the values.

# Making a copy/Modifying

we can modify a record value by doing this

```
record1 = record1 with { Price = 20 };
```

# Other datamembers

we can also add properties, fields, methods and others into records, here is our new record:

```
public record Record1(string Name, int Price)
{
    internal string firstName = Name;

    public string ProductName
    {
        get { return "fresh " + firstName; }
        init { }
    }
    public string ToFormattedString()
    {
        return string.Format("{0}: {1} From product class", Name, Price);
    }
}
```

Printing the record would output this

![image](https://github.com/user-attachments/assets/9106fad7-9e1f-4143-a42d-202fbe7c6422)

we can also use the ToFormattedString method.

# Inheritance

```
public record Record2(int id, string Name, int Price) : Record1(Name, Price);
public record Record1(string Name, int Price)
{
    internal string firstName = Name;

    public string ProductName
    {
        get { return "fresh " + firstName; }
        init { }
    }
    public string ToFormattedString()
    {
        return string.Format("{0}: {1} From product record", Name, Price);
    }
}
```

```
Console.WriteLine(r2.ToFormattedString()); //Sweets: 10 From product record
```

