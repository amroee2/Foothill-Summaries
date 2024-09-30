# Unit Testing Best Practices

Unit testing is a software testing technique where individual components or functions of a program are tested in isolation. The goal is to validate that each "unit" of the code performs as expected. Unit tests are typically automated and are run as part of the build process to ensure code quality and prevent bugs.

To get the most value out of unit tests, it's important to follow best practices. These practices help ensure that tests are effective, easy to maintain, and provide reliable feedback about your code.

## Creating Seams

A seam in software development is a place in the code where behavior can be altered without modifying the code itself. Seams allow you to isolate the parts of your code that you want to test by controlling or changing the behavior of external dependencies.

Example:

```csharp
public class WeatherService
{
    private readonly IWeatherApi _api;

    public WeatherService(IWeatherApi api)
    {
        _api = api;
    }

    public string GetWeatherForecast()
    {
        return _api.FetchForecast();
    }
}

```

```csharp
public class FlightBookingService
{
    private readonly IPaymentProcessor _paymentProcessor;

    public FlightBookingService(IPaymentProcessor paymentProcessor)
    {
        _paymentProcessor = paymentProcessor;
    }

    public bool ProcessBooking(BookingDetails details)
    {
        return _paymentProcessor.Process(details);
    }
}
```

## Best Practices

- Test One Thing at a Time (Single Responsibility in Tests)

Each unit test should focus on a single function or method. This way, you can quickly identify which part of the code is failing when a test does not pass. A good unit test ensures that the test itself is clear, concise, and targets only one specific behavior or scenario.

- Write Independent and Isolated Tests

Unit tests should not rely on external systems (such as databases, web services, or file systems) and should not depend on each other. This ensures that they can run in any order, either individually or in a suite, without causing false positives or negatives due to shared state or side effects.

Example: If a test requires a database connection, use mock objects or in-memory databases to simulate the behavior rather than connecting to a live database.

- Follow the Arrange-Act-Assert (AAA) Pattern:

The AAA pattern structures your test into three parts:

Arrange: Set up the test, including initializing the objects and setting preconditions.
Act: Execute the method or functionality being tested.
Assert: Verify that the result matches the expected behavior.

```csharp
// Arrange
var cart = new ShoppingCart();

// Act
var totalPrice = cart.CalculateTotalPrice();

// Assert
Assert.AreEqual(0, totalPrice);
```

- Use Mocks to Replace External Dependencies

When a unit of code interacts with external systems (e.g., databases, web services), you should avoid testing those dependencies in a unit test. Instead, use mocks or stubs to simulate the behavior of those systems. This isolates the code under test and ensures the test doesn’t fail due to external factors.

- Write Tests for Both Positive and Negative Scenarios

Test both the "happy path" (when everything goes right) and edge cases (when things go wrong). Negative tests validate that the code behaves correctly under invalid or unexpected conditions, such as handling null inputs, incorrect data types, or failing operations gracefully.

Example: For a login system, you should test both successful logins and unsuccessful attempts (invalid credentials, locked accounts, etc.).

- Minimize Assertions Per Test

Each test should have a minimal number of assertions (ideally one or two). The more assertions a test contains, the harder it becomes to pinpoint the cause of a failure. If multiple things need to be tested, consider breaking them into separate tests.
