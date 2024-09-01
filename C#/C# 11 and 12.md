# Primary constructors for classes

```
// C# 12 Example
public class Point(int x, int y)
{
    public int X { get; } = x;
    public int Y { get; } = y;
}
```

# Collection expressions

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

