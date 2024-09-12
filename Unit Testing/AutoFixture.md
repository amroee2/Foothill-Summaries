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

# Customizing AutoFixture

## .Inject()

The .Inject() method in AutoFixture is used to predefine specific values for a type. Once a value is injected, every instance of that type created by AutoFixture will have the injected value instead of being randomly generated. It's useful when you want to ensure that specific types always have a predefined, consistent value throughout your tests.

```csharp
var fixture = new Fixture();
fixture.Inject(42);

var number = fixture.Create<int>();
Console.WriteLine(number);  // Output: 42
```

```csharp
var fixture = new Fixture();
fixture.Inject("TestString");

var str1 = fixture.Create<string>();
var str2 = fixture.Create<string>();

Console.WriteLine(str1);  // Output: "TestString"
Console.WriteLine(str2);  // Output: "TestString"
```

```csharp
var fixture = new Fixture();
var specificPassenger = new Passenger { Name = "Amro", Age = 30 };

// Inject the specific Passenger instance
fixture.Inject(specificPassenger);

// Every time you create a Passenger, it will return the injected one
var passenger1 = fixture.Create<Passenger>();
var passenger2 = fixture.Create<Passenger>();

Console.WriteLine(passenger1.Name);  // Output: "Amro"
Console.WriteLine(passenger2.Age);   // Output: 30
```

## .Customize()

Used to customize all instances of the type passed to fixture, for example in this method, **all passenger instances have Name property = "Amro".

```csharp

        [Fact]
        public void TestPassengerName()
        {
            var fixture = new Fixture();

            // Customizing the Name property to always be "Amro"
            fixture.Customize<Passenger>(composer => composer.With(p => p.Name, "Amro"));
            var passenger = fixture.Create<Passenger>();

            var passenger2 = fixture.Create<Passenger>();

            var passenger3 = fixture.Create<Passenger>();   

            Assert.Equal("Amro", passenger.Name);
        }
```

## .Build()

Unlike .Customize, build only returns one instances with the specified customizations

Here only the first passenger has Name property set to "Amro", the others have anonymous values.

```csharp
        public void TestPassengerName()
        {
            var fixture = new Fixture();

            // Customizing the Name property to always be "Amro"
           
            var passenger = fixture.Build<Passenger>().With(p => p.Name, "Amro").Create();

            var passenger2 = fixture.Create<Passenger>();

            var passenger3 = fixture.Create<Passenger>();   

            Assert.Equal("Amro", passenger.Name);
        }
```

## .Freeze

Freezing a value ensures that the same instance is used whenever AutoFixture is asked for that type during the test. This is useful for dependencies like mock objects or commonly shared instances in a test.

```csharp
var fixture = new Fixture();

// Freezing ensures that the same email is used for every call to fixture.Create<MailAddress>()
var frozenEmail = fixture.Freeze<MailAddress>();

// Now any other object that needs an email will get the same frozen one
var passenger1 = fixture.Create<Passenger>(); // Uses frozen email
var passenger2 = fixture.Create<Passenger>(); // Uses frozen email

Console.WriteLine(passenger1.Email == passenger2.Email);  // Output: True
```

# Spicemens and AutoFixture pipleline

A specimen is any value that AutoFixture creates during the object generation process. The AutoFixture Pipeline handles the generation of specimens and can be customized using specimen builders.

![image](https://github.com/user-attachments/assets/c0c66add-e54a-4958-9d6a-d64f065631e8)

![image](https://github.com/user-attachments/assets/9e3a4248-9528-4279-889f-308a79bb1253)

![image](https://github.com/user-attachments/assets/b9015c72-4360-4c4d-8239-35041873585a)

