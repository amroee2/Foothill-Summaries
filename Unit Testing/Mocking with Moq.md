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

