# Architecture 

Architecture consists of the structure combined with architecture characteristics, architecture decisions, and design principles.

![image](https://github.com/user-attachments/assets/00519e2a-1284-4c30-b804-23b3188dd08a)

The structure of the system refers to the type of architecture style (or styles) the system is implement in (such as microservices, layered, microkernel, and so on).

Architecture characteristics refers to the “-ilities” that the system must support. All of the characteristics listed bellow do not require knowledge of the functionality of the system, yet they are required in order for the system to function properly.

![image](https://github.com/user-attachments/assets/2da9a0bd-01be-4795-997a-49cb6d548c26)

Architecture decisions are rules for constructing systems. They form the constraints of the system, and direct the development teams on what is and what isn’t allowed. (If a particular architecture decision cannot be implemented in one part of the system due to some condition/exception or other constraint, that decision (or rule) can be “broken” through something called a variance.)

![image](https://github.com/user-attachments/assets/ddcce8fd-d9af-48a4-ac76-32623dc8fee0)

Design principles are guidelines for constructing systems.

![image](https://github.com/user-attachments/assets/ef221f73-a244-4263-b00e-46522b9e69dc)

## Laws of Software Architecture

- Everything in software architecture is a tradeoff.

Nothing exists on a nice clean spectrum for software architects — every decision must take into account many opposing factors.

- Why is more important than how.

An architect can look at an existing system they have no knowledge of and ascertain how the structure of the architecture works, but will struggle explaining why certain choices were made versus others.

## Some known architectures

## Monolithic application

Monolithic archittecture is an all in one package, it combines all projects and layers into one single project that gets deployed together. It's entierly self contained, It may interact with other services or data stores in the course of performing its operations, but the core of its behavior runs within its own process and the entire application is typically deployed as a single unit. If such an application needs to scale horizontally, typically the entire application is duplicated across multiple servers or virtual machines.

Advantages:

- Simpler to develop initially
- Easier to deploy

Disadvantages: 

- Scaling: If we plan on scaling the application and allow it to handle more requests, we will have to scale the whole app, not just the part that would need more scaling.

- Single point of failure:  A small bug in one part can break the whole app.

- Challenging to maintain: As the app grows, the code can become complex and harder to manage.

In summary, a monolithic application works well for simple or small projects but can become a problem as the application grows larger and more complex. For large-scale systems, many developers prefer **microservices architecture** (discussed later), where different parts of the application are developed and deployed independently. 

## N Layered Architecture 

N layered architectures have the typical known layers: presentation layer (user interface) , application layer (business logic) and infastructure layer (data access). 

UI -> Business -> Data Access

![image](https://github.com/user-attachments/assets/a837b83a-971f-45de-9518-889293bd5c4d)

Where the request goes to the controller in the presentation layer in the form of created DTOs, then the input is validated and the service layer is called, which applies business logic and validates business rules and then calls the data access layer to fetch from a database.

The issue is that the layers are tightly coupled to each other, the application layer fully depends on the data access layer which makes it hard to test and harder to replace the infrastructure 

## Clean Architecture

Instead of the application layer depending on the infrastructure, its the opposite, the infrastructre would depend on the application layer.

UI -> Business <- Data Access

Interfaces and data models from repository pattern are moved to the application layer, forcing the data access layer to depend on it, hence giving full isolation for the application layer and easier testability.

![image](https://github.com/user-attachments/assets/691ada6f-43db-466e-a91e-e1091fb809b5)

## Vertical Slices

Vertical slices architecture looks at dividing the application based on features rather than technicalities, it groups everything related to a single action into one place

![image](https://github.com/user-attachments/assets/1f384a17-1e12-4342-bdd2-5d3812812030)

Vertical slices downside is that there is no clear way on how code can be shared between slices, so there will be violations of the DRY principle.

## Repository Pattern and Unit of work

Repository pattern refers to the concept of adding a layer between business layer and the database through repositroy classes

![image](https://github.com/user-attachments/assets/ae129d6b-6a56-4248-bd84-6574effaf8e5)

These repository classes implement an interface and interact with the database and other layers can use these interfaces to handle requests.

Unit of work is about bundling or encapsulating one or more repositories into one unit, so changes can be comitted together to the database, which reduces network traffic and valuable if one of the operations fails, with included rollback mechanism.

```csharp

public class UnitOfWork : IUnitOfWork
{
    private readonly DbContext _context;
    private IRepository<Order> _orders;

    public UnitOfWork(DbContext context)
    {
        _context = context;
    }

    public IRepository<Order> Orders => _orders ??= new Repository<Order>(_context);

    public async Task<int> CommitAsync()
    {
        return await _context.SaveChangesAsync();
    }

    public void Dispose()
    {
        _context.Dispose();
    }
}
```
