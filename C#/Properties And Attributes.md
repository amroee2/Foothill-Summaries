# Properties

Properties are the special type of class members that provides a flexible mechanism to read, write, or compute the value of a private field.

Properties can be used as if they are public data members, but they are actually special methods called accessors (getters and setters).

Properties replaced the conventional 

```
private int count;

public int getCount(){
    return count;
}
public int setCount(int number){
    this.count = number;
}
```

With this

private int count;

public int Count
{
    get { return count; }
    set { count = value; }
}

We can add conditional logic for example too.

```
private int count;

public int Count
{
    get { return count; }
    set
    {
        if (value < 0) 
            throw new ArgumentException("Count cannot be negative.");
        count = value;
    }
}
```

## Auto implemented properties

These are a shorthand way to declare a property when no additional logic is needed for the getter and setter. C# automatically generates the backing field for you.

```
public int Count { get; set; }
```
## When to use?

- Auto-Implemented Properties: Use these when you just need simple getters and setters with no additional logic (e.g., just reading and writing the value).

- Manually Implemented Properties: Use these when you need to perform additional logic.

# Attributes

In C#, attributes are a way to add metadata to your code elements (such as classes, methods, properties, etc.). This metadata provides additional information to the compiler, runtime, or external tools, which can then act based on the presence of those attributes.

```
[Obsolete("This method is deprecated. Use NewMethod instead.")]
public void OldMethod()
{
    // ...
}

public void NewMethod()
{
    // ...
}
```
```
[System.Diagnostics.Conditional("DEBUG")]
public void Log(string message)
{
    Console.WriteLine(message);
}
```

More attributes [link](https://juvenile-longship-fbf.notion.site/Attributes-39c1ad11aa7443ed837463bfe7e9fd6c)
## Custom Attributes

```
using System;

public class SimpleAttribute : Attribute
{
    public string Message { get; }

    public SimpleAttribute(string message)
    {
        Message = message;
    }
}
```

```
[Simple("This is a simple class")]
public class MyClass
{
    [Simple("This is a simple method")]
    public void MyMethod()
    {
        // Method implementation
    }
}
```

```
using System;
using System.ComponentModel.DataAnnotations;

namespace AirportTicketBookingSystem.Validation
{
    public class FutureDateAttribute : ValidationAttribute
    {
        public override bool IsValid(object value)
        {
            if (value is DateTime dateTime)
            {
                return dateTime > DateTime.Today;
            }
            return false;
        }

        public override string FormatErrorMessage(string date)
        {
            return $"The {date} must be a future date.";
        }
    }
}
```
