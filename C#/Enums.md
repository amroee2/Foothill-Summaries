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
