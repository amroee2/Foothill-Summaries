# Test Driven Development

Test Driven Development (TDD) is software development approach in which test cases are developed to specify and validate what the code will do. In simple terms, test cases for each functionality are created and tested first and if the test fails then the new code is written in order to pass the test and making code simple and bug-free.

## TDD Cycle

As mentioned before, test cases are created first and tested, and then the implementations happens and new code is written untl the test passes. After these two steps, we can go ahead and refactor the written code.

This is known as the TDD Cycle

![image](https://github.com/user-attachments/assets/b99ba57e-cc2a-4b1b-ac8a-001eb3db0cb0)

## Advantages

- Think about the APIs:

When using TDD, you design tests before writing code, which forces you to think about how your functions and methods (your APIs) will be used by others. This leads to cleaner, more usable interfaces.

- Think about what the code should do:

TDD requires you to define the desired behavior before implementing the functionality. Writing tests first forces you to clearly define what the code is supposed to accomplish, leading to more focused and intentional code.

- Get fast feedback:

Running tests gives immediate feedback on whether the code works as expected. This reduces the time spent debugging and ensures issues are identified early.

- Create modular code:

To make the code testable, TDD encourages you to write smaller, independent modules. This leads to a more modular and flexible codebase that's easier to maintain and extend.

- Write maintainable code:

The process of writing tests first often results in code that's easier to understand and maintain because you ensure it meets well-defined requirements. This makes future modifications less prone to breaking existing functionality.
Tests are documentation:

The tests themselves serve as documentation for the code. By reading the tests, other developers (or your future self) can easily understand how the code is intended to behave and what edge cases it handles.

![image](https://github.com/user-attachments/assets/0be519a1-c850-4117-9016-1b6dd8a96cc8)

# Example Program

Suppose we have a coffee place and we want to implement the functionality of being able to book a desk.

For this we need three classes:

1- DeskBookingRequest
2- DeskBookingResult
3- DeskBookingRequestProcessor

First we stard with the **unit test**

Test would look like this

```csharp

        [Fact]
        public void ShouldProcessRequests()
        {
            var request = new DeskBookingRequest
            {
                FirstName = "Amro",
                LastName = "Qadadha",
                Email = "amroqadadha@gmail.com",
                DateTime = DateTime.Now
            };
            var processor = new DeskBookingRequestProcessor();

            var response = processor.BookDesk(request);

            Assert.Equal(request.FirstName, response.FirstName);
            Assert.Equal(request.LastName, response.LastName);
            Assert.Equal(request.Email, response.Email);
            Assert.Equal(request.DateTime, response.DateTime);

        }
```

While we are writing the test the IDE will prompt us to make these 3 classes, and we can allow it to create it, after doing so, the classes will look like this.

```csharp

namespace TDD
{
    internal class DeskBookingRequestProcessor
    {
        public DeskBookingRequestProcessor()
        {
        }

        internal DeskBookingResponse BookDesk(DeskBookingRequest request)
        {
            throw new NotImplementedException();
        }
    }
}

namespace TDD
{
    internal class DeskBookingRequest
    {
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public string Email { get; set; }
        public DateTime DateTime { get; set; }
    }
}

namespace TDD
{
    internal class DeskBookingResponse
    {
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public string Email { get; set; }
        public DateTime DateTime { get; set; }
    }
}
```

![image](https://github.com/user-attachments/assets/4ca36658-0ebb-4aee-b07c-96737dcaf244)


Running the test now will make it fail

![image](https://github.com/user-attachments/assets/5fa03855-f515-46be-96e7-eba40d27b7c3)

This is the first step in the cycle, now we have to implement the BookDesk method so the test can pass

```csharp
        internal DeskBookingResponse BookDesk(DeskBookingRequest request)
        {
            return new DeskBookingResponse
            {
                FirstName = request.FirstName,
                LastName = request.LastName,
                Email = request.Email,
                DateTime = request.DateTime
            };
        }
```

![image](https://github.com/user-attachments/assets/0b85a633-51e8-428a-b8c6-08509912494e)

Then we can refactor, create a new core project, move the classes there as they do not belong in the test class, and modify the access modifiers.

And that completes a TDD Cycle.

Same process is applied again if we want to add an ArgumentNullExcepton feature instead of NullReferenceException

Test Fails
```csharp
        public void ShouldReturnArgumentNullExceptionIfRequestIsNull()
        {
            var processor = new DeskBookingRequestProcessor();

            var exception = Assert.Throws<ArgumentNullException>(() => processor.BookDesk(null));

            Assert.Equal("request", exception.ParamName);
        }
```

Add implementation

```csharp
        public DeskBookingResponse BookDesk(DeskBookingRequest request)
        {
            if(request == null)
            {
                throw new ArgumentNullException(nameof(request));
            }
            return new DeskBookingResponse
            {
                FirstName = request.FirstName,
                LastName = request.LastName,
                Email = request.Email,
                DateTime = request.DateTime
            };
        }
```

Test Passes

![image](https://github.com/user-attachments/assets/2e98610e-fda0-4228-acaf-9caf54371389)

We can add refactoring, but this time on the test class, since we initialize the processor in both tests, we can apply DRY principle to setup the processor in the constructor

Before

```csharp

namespace TDD
{
    public class DeskBookingProcessorTests
    {
        [Fact]
        public void ShouldProcessRequests()
        {
            var request = new DeskBookingRequest
            {
                FirstName = "Amro",
                LastName = "Qadadha",
                Email = "amroqadadha@gmail.com",
                DateTime = DateTime.Now
            };
            var processor = new DeskBookingRequestProcessor();

            var response = processor.BookDesk(request);

            Assert.Equal(request.FirstName, response.FirstName);
            Assert.Equal(request.LastName, response.LastName);
            Assert.Equal(request.Email, response.Email);
            Assert.Equal(request.DateTime, response.DateTime);

        }
        [Fact]
        public void ShouldReturnArgumentNullExceptionIfRequestIsNull()
        {
            var processor = new DeskBookingRequestProcessor();

            var exception = Assert.Throws<ArgumentNullException>(() => processor.BookDesk(null));

            Assert.Equal("request", exception.ParamName);
        }
    }
}
```

After

```csharp

namespace TDD
{
    public class DeskBookingProcessorTests
    {
        private DeskBookingRequestProcessor _processor;

        public DeskBookingProcessorTests()
        {
            _processor = new DeskBookingRequestProcessor();
        }
        [Fact]
        public void ShouldProcessRequests()
        {
            var request = new DeskBookingRequest
            {
                FirstName = "Amro",
                LastName = "Qadadha",
                Email = "amroqadadha@gmail.com",
                DateTime = DateTime.Now
            };

            var response = _processor.BookDesk(request);

            Assert.Equal(request.FirstName, response.FirstName);
            Assert.Equal(request.LastName, response.LastName);
            Assert.Equal(request.Email, response.Email);
            Assert.Equal(request.DateTime, response.DateTime);

        }
        [Fact]
        public void ShouldReturnArgumentNullExceptionIfRequestIsNull()
        {
            var exception = Assert.Throws<ArgumentNullException>(() => _processor.BookDesk(null));

            Assert.Equal("request", exception.ParamName);
        }
    }
}
```

# Decoupling 

We want to add the functionality to save the booking into the database, and to do this we can just create an interface that we can mock in the testing methods, so we can test methods in **isolation**

We need an interface, we can call it IDeskBookingRepository, and a new class that will represent the object saved into the database

```csharp
namespace TDD
{
    public interface IDeskBookingRepository
    {
        public void Save(DeskBooking deskBooking);
    }
}
```

```csharp
namespace TDD
{
    public class DeskBooking
    {
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public string Email { get; set; }
        public DateTime DateTime { get; set; }
    }
}
```

Test should look like this, and it will faill

```csharp
        public void ShouldStoreBooking()
        {
            var database = new Mock<IDeskBookingRepository>();
            var savedDeskBooking = new DeskBooking();
            database.Setup(x => x.Save(It.IsAny<DeskBooking>())).Callback<DeskBooking>(deskBooking =>
            {
                savedDeskBooking = deskBooking;
            });
            var response = _processor.BookDesk(_request);
            database.Verify(x => x.Save(It.IsAny<DeskBooking>()), Times.Once);
            Assert.NotNull(savedDeskBooking);
            Assert.Equal(_request.FirstName, savedDeskBooking.FirstName);
            Assert.Equal(_request.LastName, savedDeskBooking.LastName);
            Assert.Equal(_request.Email, savedDeskBooking.Email);
            Assert.Equal(_request.DateTime, savedDeskBooking.DateTime);
        }
```

Now in the next step in the cycle, we need to introduce the dependency through DIP constructor injection, call the save method in the BookDesk method, and then run the tests again. 

After applying these modifications, the test now will pass.

```csharp

namespace TDD
{
    public class DeskBookingRequestProcessor
    {
        public IDeskBookingRepository _deskBookingRepositor;
        public DeskBookingRequestProcessor(IDeskBookingRepository deskBookingRepository)
        {
            _deskBookingRepositor = deskBookingRepository;
        }

        public DeskBookingResponse BookDesk(DeskBookingRequest request)
        {
            if(request == null)
            {
                throw new ArgumentNullException(nameof(request));
            }

            _deskBookingRepositor.Save(new DeskBooking
            {
                FirstName = request.FirstName,
                LastName = request.LastName,
                Email = request.Email,
                DateTime = request.DateTime
            });

            return new DeskBookingResponse
            {
                FirstName = request.FirstName,
                LastName = request.LastName,
                Email = request.Email,
                DateTime = request.DateTime
            };
        }
    }
}
```

```csharp

using Moq;

namespace TDD
{
    public class DeskBookingProcessorTests
    {
        private readonly DeskBookingRequestProcessor _processor;
        private readonly DeskBookingRequest _request;
        private readonly Mock<IDeskBookingRepository> database;
        public DeskBookingProcessorTests()
        {
            _request = new DeskBookingRequest
            {
                FirstName = "Amro",
                LastName = "Qadadha",
                Email = "amroqadadha@gmail.com",
                DateTime = DateTime.Now
            };
             database = new Mock<IDeskBookingRepository>();
            _processor = new DeskBookingRequestProcessor(database.Object);
        }
        [Fact]
        public void ShouldProcessRequests()
        {

            var response = _processor.BookDesk(_request);

            Assert.Equal(_request.FirstName, response.FirstName);
            Assert.Equal(_request.LastName, response.LastName);
            Assert.Equal(_request.Email, response.Email);
            Assert.Equal(_request.DateTime, response.DateTime);

        }
        [Fact]
        public void ShouldReturnArgumentNullExceptionIfRequestIsNull()
        {
            var exception = Assert.Throws<ArgumentNullException>(() => _processor.BookDesk(null));

            Assert.Equal("request", exception.ParamName);
        }
        [Fact]
        public void ShouldStoreBooking()
        {
            var savedDeskBooking = new DeskBooking();
            database.Setup(x => x.Save(It.IsAny<DeskBooking>())).Callback<DeskBooking>(deskBooking =>
            {
                savedDeskBooking = deskBooking;
            });
            var response = _processor.BookDesk(_request);
            database.Verify(x => x.Save(It.IsAny<DeskBooking>()), Times.Once);
            Assert.NotNull(savedDeskBooking);
            Assert.Equal(_request.FirstName, savedDeskBooking.FirstName);
            Assert.Equal(_request.LastName, savedDeskBooking.LastName);
            Assert.Equal(_request.Email, savedDeskBooking.Email);
            Assert.Equal(_request.DateTime, savedDeskBooking.DateTime);
        }
    }
}
```

Now we can refactor the code by introducing a DeskBookingBaseClass, where we can add all the booking attributes in it and allow ```DeskBookingRequest```, ```DeskBookingResponse``` and ```DeskBooking``` class to inherit from.

We can also introduce a new method to apply DRY principle in DeskBookingProcessor class

New modifications

```csharp
namespace DeskBooking
{
    public class DeskBookingBase
    {
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public string Email { get; set; }
        public DateTime DateTime { get; set; }
    }
}
```
```csharp
using DeskBooking;

namespace TDD
{
    public class DeskBooking : DeskBookingBase
    {
    }
}

using DeskBooking;

namespace TDD
{
    public class DeskBookingRequest : DeskBookingBase
    {
    }
}

using DeskBooking;

namespace TDD
{
    public class DeskBookingResponse : DeskBookingBase
    {
    }
}
```

```csharp

using DeskBooking;

namespace TDD
{
    public class DeskBookingRequestProcessor
    {
        public IDeskBookingRepository _deskBookingRepositor;
        public DeskBookingRequestProcessor(IDeskBookingRepository deskBookingRepository)
        {
            _deskBookingRepositor = deskBookingRepository;
        }

        public DeskBookingResponse BookDesk(DeskBookingRequest request)
        {
            if(request == null)
            {
                throw new ArgumentNullException(nameof(request));
            }

            _deskBookingRepositor.Save(CreateBooking<DeskBooking>(request));

            return CreateBooking<DeskBookingResponse>(request);
        }
        public T CreateBooking<T>(DeskBookingBase desk) where T : DeskBookingBase, new()
        {
            return new T
            {
                FirstName = desk.FirstName,
                LastName = desk.LastName,
                Email = desk.Email,
                DateTime = desk.DateTime
            };
        }
    }
}
```
