# AutoFixture 

AutoFixture is a library focused on test data generation so that unit tests can focus on the behavior to be tested rather than on the plumbing needed to get the test to run.

# Why Auto Fixture?

Assume we have these classes

In this case, we have to manually create and assign values to each property of the Passenger object and its nested properties. This can become more complicated when you need to test different passengers with different data. Also, if the object structure changes, you will need to adjust each test manually.

```csharp
public class Passenger
{
    public string Name { get; set; }
    public int Age { get; set; }
    public Address Address { get; set; }
    public ContactInfo ContactInfo { get; set; }
}

public class Address
{
    public string Street { get; set; }
    public string City { get; set; }
}

public class ContactInfo
{
    public string PhoneNumber { get; set; }
    public string Email { get; set; }
}

// Test class
public class FlightBookingServiceTests
{
    [Fact]
    public void BookFlight_ShouldProcessValidPassenger()
    {
        // Manually creating test inputs
        var passenger = new Passenger
        {
            Name = "John Doe",
            Age = 30,
            Address = new Address
            {
                Street = "123 Main St",
                City = "New York"
            },
            ContactInfo = new ContactInfo
            {
                PhoneNumber = "555-1234",
                Email = "john.doe@example.com"
            }
        };

        var flightBookingService = new FlightBookingService();

        // Act
        flightBookingService.BookFlight(passenger);

        // Assert (for example)
        Assert.True(flightBookingService.IsFlightBooked(passenger));
    }
}
```

With Auto Fixture

We can initialize an instance from the ```Fixture``` class (from AutoFixture package), and then use it to create a new Passenger instance and simply pass it to a BookFlight method.
```csharp
    [Fact]
    public void BookFlight_ShouldProcessValidPassenger()
    {
        // Using AutoFixture to generate test data
        var fixture = new Fixture();
        var passenger = fixture.Create<Passenger>();

        var flightBookingService = new FlightBookingService();

        // Act
        flightBookingService.BookFlight(passenger);

        // Assert (for example)
        Assert.True(flightBookingService.IsFlightBooked(passenger));
    }
```

In the first scenario, any modifications to the passenger class would have forced us to update all unit testing methods.

# AutoFixture with different types

When we allow AutoFixture to create a value, this value is labaled as "Anonymous" 

## Anonymous Strings

```csharp
var fixture = new Fixture();
var randomString = fixture.Create<string>();
Console.WriteLine(randomString);
```

## Anonymous Numbers

```csharp
var randomInt = fixture.Create<int>();
var randomDouble = fixture.Create<double>();
Console.WriteLine(randomInt);  
Console.WriteLine(randomDouble);
```

## Anonymous Date and Time

```csharp
var randomDateTime = fixture.Create<DateTime>();
Console.WriteLine(randomDateTime);
```

## Anonymous Enums and Guids

Guid (Globally Unique Identifier) is a 128-bit (16-byte) number that is used to uniquely identify objects or entities across systems.

```csharp
// Enum example
public enum FlightStatus { OnTime, Delayed, Cancelled }
var randomEnum = fixture.Create<FlightStatus>();
Console.WriteLine(randomEnum);  // Output: random value from the enum

// GUID example
var randomGuid = fixture.Create<Guid>();
Console.WriteLine(randomGuid);  // Output: random GUID
```

## Anonymous Emails

```csharp
var randomEmail = fixture.Create<MailAddress>().Address;
Console.WriteLine(randomEmail);  // Output: random email like "random.person@example.com"
```

We can also access each part of the email 

```csharp
using System.Net.Mail;

var fixture = new Fixture();
var mailAddress = fixture.Create<MailAddress>();

// Access the full address
string fullAddress = mailAddress.Address;
Console.WriteLine($"Full Address: {fullAddress}");

// Access the local part (User)
string localPart = mailAddress.User;
Console.WriteLine($"Local Part: {localPart}");

// Access the domain part (Host)
string domainPart = mailAddress.Host;
Console.WriteLine($"Domain Part: {domainPart}");
```

## Create Sequence of Anon Types

```csharp
var randomIntegers = fixture.CreateMany<int>(5).ToList();
Console.WriteLine(string.Join(", ", randomIntegers));  // Output: list of 5 random integers
```

## Anonymous instance of a custom type

```csharp
public class Passenger
{
    public string Name { get; set; }
    public int Age { get; set; }
}

var randomPassenger = fixture.Create<Passenger>();
Console.WriteLine($"{randomPassenger.Name}, {randomPassenger.Age}");  // Output: random name and age
```

## AutoFixture with DataAnnotations 

```csharp
public class AnnotatedPassenger
{
    [StringLength(10)]
    public string Name { get; set; }
    
    [Range(18, 60)]
    public int Age { get; set; }
}

var randomAnnotatedPassenger = fixture.Create<AnnotatedPassenger>();
Console.WriteLine($"{randomAnnotatedPassenger.Name}, {randomAnnotatedPassenger.Age}");
```
