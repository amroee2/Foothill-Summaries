# C# 11

## Required

```
public class Person
{
    public required string Name { get; init; }
    public int Age { get; init; }
}
var person = new Person { Name = "Amro", Age = 22 }; // Name is required
```
## Generic attributes
```
public class ExampleAttribute<T> : Attribute { }

[Example<int>]
public class MyClass { }
```
# C# 12

## Primary constructors for classes

```
// C# 12 Example
public class Point(int x, int y)
{
    public int X { get; } = x;
    public int Y { get; } = y;
}
```

## Collection expressions

```
// Create an array:
int[] a = [1, 2, 3, 4, 5, 6, 7, 8];

// Create a list:
List<string> b = ["one", "two", "three"];

// Create a span
Span<char> c  = ['a', 'b', 'c', 'd', 'e', 'f', 'h', 'i'];

// Create a jagged 2D array:
int[][] twoD = [[1, 2, 3], [4, 5, 6], [7, 8, 9]];

// Create a jagged 2D array from variables:
int[] row0 = [1, 2, 3];
int[] row1 = [4, 5, 6];
int[] row2 = [7, 8, 9];
int[][] twoDFromVariables = [row0, row1, row2];
```

## Spread element

```
int[] row0 = [1, 2, 3];
int[] row1 = [4, 5, 6];
int[] row2 = [7, 8, 9];
int[] single = [.. row0, .. row1, .. row2];
foreach (var element in single)
{
    Console.Write($"{element}, ");
}
// output:
// 1, 2, 3, 4, 5, 6, 7, 8, 9,
```
## Interceptors

An interceptor is a method which can declaratively substitute a call to an interceptable method with a call to itself at compile time. 

```
using System;
using System.Runtime.CompilerServices;

var c = new C();
c.InterceptableMethod(1); // L1: prints "interceptor 1"
c.InterceptableMethod(1); // L2: prints "other interceptor 1"
c.InterceptableMethod(2); // L3: prints "other interceptor 2"
c.InterceptableMethod(1); // prints "interceptable 1"

class C
{
    public void InterceptableMethod(int param)
    {
        Console.WriteLine($"interceptable {param}");
    }
}

// generated code
static class D
{
    [InterceptsLocation(version: 1, data: "...(refers to the call at L1)")]
    public static void InterceptorMethod(this C c, int param)
    {
        Console.WriteLine($"interceptor {param}");
    }

    [InterceptsLocation(version: 1, data: "...(refers to the call at L2)")]
    [InterceptsLocation(version: 1, data: "...(refers to the call at L3)")]
    public static void OtherInterceptorMethod(this C c, int param)
    {
        Console.WriteLine($"other interceptor {param}");
    }
}
```


## Default value for lambda expressions
```
// C# 12 Example
Func<int, int, int> add = (x = 0, y = 0) => x + y;
Console.WriteLine(add()); // Outputs 0
```

## Type alias

```
// Aliasing a type for brevity
using IntList = System.Collections.Generic.List<int>;

// Now you can use 'IntList' instead of 'List<int>'
IntList numbers = new IntList { 1, 2, 3, 4, 5 };
Console.WriteLine(string.Join(", ", numbers)); // Outputs: 1, 2, 3, 4, 5
```

