# Mocking

Mocking is a technique used in unit testing to isolate the system under test (SUT) by replacing its dependencies with controlled and predictable substitutes called "mocks." This allows you to test the behavior of the SUT (System Under Test) in isolation without relying on external factors like databases, APIs, or complex business logic in other parts of the system.

Why Mocking Is Important:
- Isolation: You can test a unit of code without depending on real services or resources, which might be slow, unreliable, or unavailable.
- Predictability: You can control the behavior of dependencies, ensuring they return known, fixed values, so your tests are deterministic.
- Focus: Mocking allows you to focus on testing the behavior of the code in isolation from the rest of the system.

# Moq

Moq is one of the most popular mocking libraries for .NET, which helps in creating mocks, stubs, and fakes easily, allowing for flexible and readable unit tests. It provides a fluent API for setting up mock objects and verifying interactions with them.

Assume we have this class

```csharp
// OrderService.cs
public class OrderService
{
    private readonly IInventoryService _inventoryService;

    public OrderService(IInventoryService inventoryService)
    {
        _inventoryService = inventoryService;
    }

    public bool PlaceOrder(int productId)
    {
        if (_inventoryService.IsProductInStock(productId))
        {
            // Logic to place order
            return true;
        }
        return false;
    }
    public bool CheckIfValid(string str)
    {
        if (str.Equals(_inventoryService.IsValid)) 
        {
            return true;
        }
        return false;
    }
}
```

Where it depends on this interface

```csharp
public interface IInventoryService
{
    bool IsProductInStock(int productId);

    public string IsValid { get; set; }
}
```

In real world scenarios, we would want an inventoryService class/interface to have its own implementations, but sometimes we would want to test a class when the dependencies are not ready, or they are but we want to test in **isolation**, and this can be done through mocking

Assume this unit testing method

We define the mocking value first using Mock<T> (generics), and then **setup** the value we want its functionality to have.

In this example, we set any integer that is passed to the ```IsProductInStock``` method to set it as true, **notice that the said method has no implementation in the interface**, this whole thing is part of the **Arrange** process.

After defining an instance of the orderService class using the .Object property for mocked values, we do the **Act** part (any int value would not matter as we already set the mocking to always return true)

Finally we can assert the result, and make sure that the mocking IsProductInStock method was accessed through the Verify method in the end

This test passes

```csharp
    [Fact]
    public void PlaceOrder_WhenProductIsInStock_ShouldReturnTrue()
    {
        // Arrange
        var inventoryServiceMock = new Mock<IInventoryService>();
        inventoryServiceMock.Setup(x => x.IsProductInStock(It.IsAny<int>())).Returns(true);

        var orderService = new OrderService(inventoryServiceMock.Object);

        // Act
        var result = orderService.PlaceOrder(1);

        // Assert
        Assert.True(result);
        inventoryServiceMock.Verify(x => x.IsProductInStock(1), Times.Once);
    }
```

## Loose Vs Strict Moqs

- Loose mocks (default in Moq): Methods return default values (like null for objects, 0 for integers) when not explicitly set up.
- Strict mocks: Every method that is called must be explicitly set up, or the mock will throw an exception if an unexpected method is called.

Example

Assume we have this same method, but this time we always return **false**

```csharp
    [Fact]
    public void PlaceOrder_WhenProductIsNotInStock_ShouldReturnFalse()
    {
        // Arrange
        var inventoryServiceMock = new Mock<IInventoryService>();
        inventoryServiceMock.Setup(x => x.IsProductInStock(It.IsAny<int>())).Returns(false);

        var orderService = new OrderService(inventoryServiceMock.Object);

        // Act
        var result = orderService.PlaceOrder(1);

        // Assert
        Assert.False(result);
        inventoryServiceMock.Verify(x => x.IsProductInStock(1), Times.Once);
    }
```

This test passes, but we don't need to setup in this method as ```IsProductInStock``` is a **boolean** method, which means it will return false by default.

This test also passes.

```csharp
    [Fact]
    public void PlaceOrder_WhenProductIsNotInStock_ShouldReturnFalse()
    {
        // Arrange
        var inventoryServiceMock = new Mock<IInventoryService>();

        var orderService = new OrderService(inventoryServiceMock.Object);

        // Act
        var result = orderService.PlaceOrder(1);

        // Assert
        Assert.False(result);
        inventoryServiceMock.Verify(x => x.IsProductInStock(1), Times.Once);
    }
```

This default behavior is part of **Loose** mode in Moq.

Using Strict mode

```csharp
    [Fact]
    public void PlaceOrder_WhenProductIsNotInStock_ShouldReturnFalse_StrictMock()
    {
        // Arrange
        var inventoryServiceMock = new Mock<IInventoryService>(MockBehavior.Strict);
        inventoryServiceMock.Setup(x => x.IsProductInStock(It.IsAny<int>())).Returns(false);

        var orderService = new OrderService(inventoryServiceMock.Object);

        // Act
        var result = orderService.PlaceOrder(1);

        // Assert
        Assert.False(result);
        inventoryServiceMock.Verify(x => x.IsProductInStock(1), Times.Once);
    }
```

This test uses strict mode, which means that **every method in the interface must be implemented in the mocking process, otherwise it will cause an exception**

If we where to remove the setup line, we would get this when running the test:

![image](https://github.com/user-attachments/assets/baac7a61-bef4-43c9-beb0-231ece0b6a4b)

If any new method was added into the interface, **it must be implemented**, even if its not called or used during the testing process.

## Tracking changes

By default, when you setup a mocking value without using the **setup** keyword, it will not be "saved"

This test **does not pass**

```csharp

    public void CheckIfValid_WhenStringIsValid_ShouldReturnTrue()
    {
        // Arrange
        var inventoryServiceMock = new Mock<IInventoryService>();
        inventoryServiceMock.Object.IsValid = "valid";

        var orderService = new OrderService(inventoryServiceMock.Object);

        // Act
        var result = orderService.CheckIfValid("valid");

        // Assert
        Assert.Equal("valid", inventoryServiceMock.Object.IsValid);
    }

```

When using the Setup we talked about before, the changes are tracked, and it will work fine, but another way to do this is through ```mock.SetupAllProperties()```

This test passes

```csharp
    public void CheckIfValid_WhenStringIsValid_ShouldReturnTrue()
    {
        // Arrange
        var inventoryServiceMock = new Mock<IInventoryService>();
        inventoryServiceMock.SetupAllProperties();  // Automatically tracks all property changes
        inventoryServiceMock.Object.IsValid = "valid";

        var orderService = new OrderService(inventoryServiceMock.Object);

        // Act
        var result = orderService.CheckIfValid("valid");

        // Assert
        Assert.Equal("valid", inventoryServiceMock.Object.IsValid);
    }
```

SetupAllProperties also gives all properties their default values (0 for int, false for boolean...).
