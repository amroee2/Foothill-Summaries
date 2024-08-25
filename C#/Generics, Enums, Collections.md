# Generics

Generics in C# provide a powerful way to define classes, interfaces, methods, and delegates with a placeholder for the type of data they store or use. This allows you to write more flexible and reusable code that can operate on various data types while ensuring type safety at compile-time.

## Generic classes

Generic classes can be initialized like this.

Notice how generic type can also be passed as parameters and as a method type.

![image](https://github.com/user-attachments/assets/4782daad-2b5f-458d-9734-b4b87f1c7386)

Through the same class, we can declare a list of strings and integers.

![image](https://github.com/user-attachments/assets/38e4dbe2-5ffe-45d7-b3e2-ac109158ee50)

We can also have multiple parameters

```
class KeyValuePair<TKey, TValue>
{
    public TKey Key { get; set; }
    public TValue Value { get; set; }
}
```

## Generic Methods

- Methods that can work with any data type.
- The type parameter is specified when you call the method.

![image](https://github.com/user-attachments/assets/45595af8-a570-4ce4-9f0c-64b707e4d737)

![image](https://github.com/user-attachments/assets/a8258480-14bf-4c2b-b31e-73d6037085a6)

![image](https://github.com/user-attachments/assets/b8aec32a-3a15-4ddc-b17c-633c02dee41e)

# Enums

An enum (short for enumeration) is a distinct value type in C# that defines a set of named constants, typically used to represent a collection of related values that are known at compile time. 
```
public enum Day
{
    Sunday, //0
    Monday, //1
    Tuesday, //2
    Wednesday, //3
    Thursday, //4
    Friday, //5
    Saturday //6
}
```

By default, the type Enums use are integers, but we can also specify the underlying type
```
public enum Day : byte
{
    Sunday = 1, // You can explicitly set values
    Monday = 2,
    Tuesday = 3,
    // Remaining values will auto-increment
}
```

It's also possible to assign custom values to enums as well

```
public enum ErrorCode
{
    None = 0,
    NotFound = 404,
    ServerError = 500
}
```
## Enums in switch statements

```
Day today = Day.Monday;

switch (today)
{
    case Day.Monday:
        Console.WriteLine("It's Monday!");
        break;
    case Day.Friday:
        Console.WriteLine("It's Friday!");
        break;
    default:
        Console.WriteLine("It's another day.");
        break;
}
```
## Converting enums

```
Day today = Day.Tuesday;
int numericValue = (int)today;  // Enum to int conversion

Day dayFromValue = (Day)3;      // Int to enum conversion
```

## Enum methods

- Enum.GetValues(): Returns an array of all the values in an enum.
- Enum.IsDefined(): Checks if a given value is defined in an enum.

```
Day today = Day.Wednesday;
Console.WriteLine(today.ToString()); // Output: "Wednesday"

foreach (Day day in Enum.GetValues(typeof(Day)))
{
    Console.WriteLine(day); // Prints all days in the enum
}
```

# Collections

In C#, collections are used to store, manage, and manipulate groups of related objects. The .NET framework provides a variety of collection types, each designed to handle specific scenarios.

# Non-Generic collections

Non-generic collections were introduced in early versions of .NET and are found in the System.Collections namespace. They store elements as objects (object type), meaning they can hold any type of data. 

- They are not type safe, we would need to cast them to be able to work with the element inside.
- Relies on Boxing-Unboxing, which can impact performance

**Arraylists**
```
ArrayList list = new ArrayList();
list.Add(1);
list.Add("Hello");
int num = (int)list[0];  // Requires casting
```

**Hashtable**

```
Hashtable table = new Hashtable();
table.Add(1, "One");
string value = (string)table[1];  // Requires casting
```

And others, notice how in nowhere the type of the elements is specified.

# Generic collections

Generic collections, introduced in .NET 2.0 and found in the System.Collections.Generic namespace, provide type safety and better performance. They are strongly typed, meaning they only accept a specified data type, eliminating the need for casting and reducing the risk of runtime errors.

- Type safe since we specify the element we want to hold.
- No boxing/unboxing = better performance

**list**

```
List<int> list = new List<int>();
list.Add(1);
int num = list[0];  // No casting needed
```
**Dictionary**

```
Dictionary<int, string> dict = new Dictionary<int, string>();
dict.Add(1, "One");
string value = dict[1];  // No casting needed
```

Each collection has built in method to be able to add, remove and manipulate data within it.

Arraylist methods for example

```
ArrayList list = new ArrayList();
list.Add(1); // Adds 1 to the list
list.Insert(0, "Hello"); //Inserts Hello at the specified index
list.remove(1); // Removes the first occurnce of 1
list.RemoveAt(0); // Removes object at index 0
list.Clear(); // Removes all elements
```
