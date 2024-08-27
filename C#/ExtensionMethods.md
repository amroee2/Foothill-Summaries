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

