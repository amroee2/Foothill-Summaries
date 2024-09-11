# Fluent Assertion

Fluent Assertions in C# is a powerful library that provides an intuitive, readable way to write assertions in unit tests. It allows you to express test assertions in a natural language style, making your tests more readable and maintainable. 

Key Features of Fluent Assertions:
- Readability: The syntax is designed to be expressive and readable.
- Extensibility: You can create custom assertions and extend the library to fit your needs.
- Comprehensive assertions: It covers a wide range of data types, including objects, collections, strings, exceptions, and more.
- Detailed error messages: When an assertion fails, Fluent Assertions provides detailed and clear failure messages.

# Examples

## Simple Assertions

```csharp
int result = 5;
result.Should().Be(5);  // Asserts that result is equal to 5
```

```csharp
string name = "Fluent Assertions";
name.Should().StartWith("Fluent").And.EndWith("Assertions");
name.Should().Contain("Assertions").And.HaveLength(18);
```

```csharp
var numbers = new[] { 1, 2, 3, 4, 5 };
numbers.Should().HaveCount(5)
    .And.Contain(3)
    .And.BeInAscendingOrder();
```

## Asserting Exceptions

```csharp
Action act = () => throw new InvalidOperationException("Invalid operation");

act.Should().Throw<InvalidOperationException>()
    .WithMessage("Invalid operation");
```

```csharp
Action act = () => { /* no exception */ };
act.Should().NotThrow();
```

## Object Comparisons

```csharp
var expected = new { Name = "John", Age = 30 };
var actual = new { Name = "John", Age = 30 };

actual.Should().BeEquivalentTo(expected);
```

## Nullable Type

```csharp

int? someValue = 5;
someValue.Should().HaveValue().And.Be(5);

int? noValue = null;
noValue.Should().NotHaveValue();
```

## Time

```csharp
DateTime now = DateTime.Now;
now.Should().BeAfter(DateTime.MinValue)
    .And.BeBefore(DateTime.MaxValue);

DateTime yesterday = DateTime.Now.AddDays(-1);
yesterday.Should().BeBefore(now);
```

## Boolean

```csharp
bool isValid = true;
isValid.Should().BeTrue();

bool isEmpty = false;
isEmpty.Should().BeFalse();
```

## Custom Assertion Messages

```csharp
int value = 10;
value.Should().Be(5, "because we want to test the failure case here");
```

## Asserting Type

```csharp
object obj = "hello";
obj.Should().BeOfType<string>();

obj.Should().NotBeOfType<int>();
```

## Asserting Collections

```csharp
var fruits = new List<string> { "Apple", "Banana", "Cherry" };

// Assert that the collection contains a specific item
fruits.Should().Contain("Apple");

// Assert that all items match a condition
fruits.Should().OnlyHaveUniqueItems();

// Assert that the collection does not contain certain items
fruits.Should().NotContain("Mango");

// Assert collection is ordered
fruits.Should().BeInAscendingOrder();
```

## Testing Example

```csharp
using FluentAssertions;
using Xunit;

public class CalculatorTests
{
    [Fact]
    public void Add_ShouldReturnCorrectSum()
    {
        // Arrange
        var calculator = new Calculator();

        // Act
        int result = calculator.Add(2, 3);

        // Assert
        result.Should().Be(5);
    }
}

public class Calculator
{
    public int Add(int a, int b) => a + b;
}
```
