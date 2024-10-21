# EF Core

Entity Framework Core (EF Core) is a lightweight, cross-platform, and modern version of Microsoft’s Object-Relational Mapper (ORM) for .NET applications. It allows developers to interact with a database using .NET objects (entities) instead of manually writing SQL queries. EF Core simplifies data access by mapping database tables to C# classes and handling database interactions behind the scenes.

# Why Do We Need Frameworks for ORMs?

ORM frameworks like EF Core provide several key benefits:

- Productivity: By automating data access tasks (e.g., SQL query generation), developers can focus on writing business logic rather than repetitive database interactions.

- Abstraction: ORM abstracts the database logic, allowing developers to work with familiar object-oriented concepts (classes and properties) rather than raw SQL. This abstraction layer enables seamless transitions between different databases without changing the application code.

- Consistency: ORM frameworks provide a consistent way to interact with databases, making it easier to write, maintain, and scale applications. Developers don’t need to write custom SQL for each CRUD (Create, Read, Update, Delete) operation.

- Database Independence: ORMs abstract away database-specific nuances. You can switch from SQL Server to PostgreSQL, for instance, by updating the connection string and making minimal code changes.

- Change Tracking: ORMs like EF Core manage object states (e.g., new, modified, deleted) and automatically generate the necessary SQL to sync changes with the database.

- Migrations: EF Core includes support for database migrations, which allow developers to version and manage schema changes programmatically. This prevents manual errors when altering database structures.

# DB Context

We can control the flow between our application and database through DB context class.

DbContext is the central class that manages interactions between the application and the database. It’s responsible for tracking entity changes, managing connections, and executing database commands.

## The Goal of DbContext:

- Database Connection Management: The DbContext opens a connection to the database when needed, manages transactions, and ensures that resources are properly disposed of.
Change Tracking: DbContext keeps track of changes made to the entities (e.g., added, modified, deleted) and generates the corresponding SQL statements when SaveChanges() is called.

- Querying: It provides access to the database using LINQ queries (through DbSet properties), making it easy to retrieve and manipulate data.
Entity Set Representation: A DbContext contains DbSet<TEntity> properties that represent collections of entities (tables in the database).

- Migrations: It facilitates applying database schema migrations by mapping changes in your C# models to database schema modifications.

## Connection String

The connection string in EF Core is a critical configuration that tells the application how to connect to a database. It typically includes information like the database provider, server location, database name, authentication method, and any other necessary parameters. Here’s an example:

```csharp
        protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
        {
            if (!optionsBuilder.IsConfigured)
            {
                optionsBuilder.UseSqlServer(
                    @"Server=(localdb)\mssqllocaldb;Database=RestaurantReservationSystem;Integrated Security=True");
            }
        }
```

Goal of the Connection String:

- Establish a Connection: The connection string ensures that EF Core can connect to the specified database instance.
Database Provider Identification: EF Core can work with multiple databases (SQL Server, MySQL, PostgreSQL, etc.), and the connection string specifies which provider should be used.

- Authentication: It contains credentials to authenticate the application with the database.
  
- Configuration: Some advanced parameters in the connection string can specify timeout settings, pooling options, and encryption.

The connection string is often stored in the appsettings.json file in .NET Core projects, making it easy to manage across environments (development, staging, production).

## DbSet

DbSet represents a collection of entities from the database that you want to query or manipulate. It acts as a bridge between the application and the corresponding database table, allowing CRUD operations (Create, Read, Update, Delete) to be performed on the entities.

DbContext class manages the interaction with the database. Within the DbContext, each DbSet represents a table in the database, and the entities within the DbSet map to the rows of that table.

```csharp
public DbSet<CustomerReservationsByRestaurant> CustomerReservationsByRestaurants { get; set; }
public DbSet<Restaurant> Restaurants { get; set; }
public DbSet<Reservation> Reservations { get; set; }
public DbSet<Customer> Customers { get; set; }
public DbSet<Employee> Employees { get; set; }
public DbSet<MenuItem> MenuItems { get; set; }
public DbSet<Order> Orders { get; set; }
public DbSet<Table> Tables { get; set; }
public DbSet<OrderItem> OrderItems { get; set; }
```
## Fluent API

Through Fluent API, we can set relationships, seed data and define constraints on properties.

Fluent API is typically used inside the OnModelCreating() method of the DbContext class, allowing precise control over how entities are mapped to the database.

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Customer>()
        .Property(c => c.FirstName)
        .HasMaxLength(100)
        .IsRequired();
}
```

```csharp
           modelBuilder.Entity<Customer>().HasData(
               new Customer { CustomerId = 1, FirstName = "John", LastName = "Doe", Email = "john.doe@example.com", PhoneNumber = "123456789" },
               new Customer { CustomerId = 2, FirstName = "Jane", LastName = "Smith", Email = "jane.smith@example.com", PhoneNumber = "987654321" },
               new Customer { CustomerId = 3, FirstName = "Alice", LastName = "Johnson", Email = "alice.johnson@example.com" },
               new Customer { CustomerId = 4, FirstName = "Bob", LastName = "Brown", Email = "bob.brown@example.com", PhoneNumber = "456123789" },
               new Customer { CustomerId = 5, FirstName = "Charlie", LastName = "White", Email = "charlie.white@example.com" },
               new Customer { CustomerId = 6, FirstName = "Emily", LastName = "Davis", Email = "emily.davis@example.com", PhoneNumber = "789456123" },
               new Customer { CustomerId = 7, FirstName = "David", LastName = "Wilson", Email = "david.wilson@example.com" },
               new Customer { CustomerId = 8, FirstName = "Grace", LastName = "Taylor", Email = "grace.taylor@example.com", PhoneNumber = "321654987" },
               new Customer { CustomerId = 9, FirstName = "Ethan", LastName = "Anderson", Email = "ethan.anderson@example.com" },
               new Customer { CustomerId = 10, FirstName = "Olivia", LastName = "Moore", Email = "olivia.moore@example.com", PhoneNumber = "159753258" }
           );
```

```csharp
modelBuilder.Entity<CustomerReservationsByRestaurant>().HasNoKey().ToView("CustomersReservationByRestaurant");
```

```csharp
  modelBuilder.Entity<Customer>()
      .HasMany(c => c.Reservations)
      .WithOne(r => r.Customer)
      .OnDelete(DeleteBehavior.Cascade);
  modelBuilder.Entity<Reservation>()
      .HasMany(c => c.Orders)
      .WithOne(o => o.Reservation)
      .OnDelete(DeleteBehavior.Cascade);
  modelBuilder.Entity<Table>()
      .HasMany(t => t.Reservations)
      .WithOne(r => r.Table)
      .OnDelete(DeleteBehavior.Cascade);
  modelBuilder.Entity<Restaurant>()
      .HasMany(r => r.Employees)
      .WithOne(e => e.Restaurant)
      .OnDelete(DeleteBehavior.NoAction);
  modelBuilder.Entity<Restaurant>()
      .HasMany(r => r.Tables)
      .WithOne(t => t.Restaurant)
      .OnDelete(DeleteBehavior.NoAction);
```

# Migrations

Migrations allow you to evolve the database schema as your application evolves. Instead of manually altering the database, EF Core lets you apply schema changes through code using migrations.

```Add-Migration InitialCreate```

```Update-Database```

EF Core generates a Designer Class (often found as ModelSnapshot in the Migrations folder) during migrations. This class represents the current state of the model, helping EF Core compare the current model to the database schema and identify changes.

The Designer Class contains the model's structure and helps EF Core understand how to update the schema without relying on the previous migration files.


# LINQ Operations in ORM

We can access and manipulate data fetched from DB Context using LINQ Operations using OOP Syntax.

**Get all data**

```csharp
return await _context.Customers.ToListAsync();
```

**Get a specific element**

```csharp
return await _context.Customers.FirstOrDefaultAsync(c => c.CustomerId == id);
```

**Create an element in the database**

```csharp
await _context.Customers.AddAsync(customer);
await _context.SaveChangesAsync();
```

**Update an element**

```csharp
_context.Customers.Update(customer);
await _context.SaveChangesAsync();
```

**Delete an element**

```csharp
_context.Customers.Remove(customer);
await _context.SaveChangesAsync();
```

# EF Core Tracking and Untacking

## Tracking

By default, when entities are retrieved from the database, EF Core tracks them. This means it watches for changes to the entity's properties, and when SaveChanges() is called, it generates the appropriate SQL to update the database with those changes.

```csharp
var customer = dbContext.Customers.FirstOrDefault(c => c.Id == 1);
customer.FirstName = "NewName";
dbContext.SaveChanges();
```

## Untracking

- If you are only querying data without intending to modify it, you can use AsNoTracking() to improve performance. Untracked entities are faster to query because EF Core doesn’t need to track their state for changes.

- This is helpful for read-only operations or when you don’t plan to save changes.

```csharp
var customers = dbContext.Customers.AsNoTracking().Where(c => c.Age > 30).ToList();
```

Tracked entities are more expensive in terms of memory and performance because EF Core needs to monitor their state, while untracked entities are lighter and ideal for data retrieval where no modifications are needed.

# Modeling Relationships in EF Core

## One To One relationship

```csharp
public class Student
{
    public int Id { get; set; }
    public string Name { get; set; }
    public Address Address { get; set; }  // Navigation property
}

public class Address
{
    public int StudentId { get; set; }  // Primary key and foreign key
    public string Street { get; set; }
    public Student Student { get; set; }
}
```

**Fluent API**

```csharp
modelBuilder.Entity<Student>()
    .HasOne(s => s.Address)
    .WithOne(a => a.Student)
    .HasForeignKey<Address>(a => a.StudentId);
```

## One to Many Relationship

```csharp
public class Customer
{
    public int Id { get; set; }
    public string Name { get; set; }
    public List<Order> Orders { get; set; }  // Navigation property
}

public class Order
{
    public int Id { get; set; }
    public string Product { get; set; }
    public int CustomerId { get; set; }  // Foreign key
    public Customer Customer { get; set; }
}
```
**Fluent API**

```csharp
modelBuilder.Entity<Order>()
    .HasOne(o => o.Customer)
    .WithMany(c => c.Orders)
    .HasForeignKey(o => o.CustomerId);
```

## Many to Many Relationship

```csharp
public class Student
{
    public int Id { get; set; }
    public string Name { get; set; }
    public List<Course> Courses { get; set; }  // Navigation property
}

public class Course
{
    public int Id { get; set; }
    public string Title { get; set; }
    public List<Student> Students { get; set; }  // Navigation property
}
```

**Fluent API**

```csharp
modelBuilder.Entity<Student>()
    .HasMany(s => s.Courses)
    .WithMany(c => c.Students);
```

# Logging

Logging is essential in EF Core for monitoring database interactions, diagnosing performance issues, and troubleshooting errors. EF Core provides built-in support for logging database queries and commands.

```csharp
public class ApplicationDbContext : DbContext
{
    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        optionsBuilder
            .UseSqlServer("YourConnectionString")
            .LogTo(Console.WriteLine);
    }
}
```

# Types of loading

## Eager Loading

Eager Loading loads related entities along with the main entity as part of the initial query. This is achieved using the Include() method in LINQ queries. The goal of eager loading is to minimize the number of database queries by fetching all related data in a single query.

**How It Works?**

When you use eager loading, EF Core sends a query with JOIN or additional SELECT statements to load the main entity and its related data together.

```csharp

public async Task<List<MenuItem>> GetMenuItemsByReservationIdAsync(int reservationId)
{
    var menuItems = await _context.Orders.AsNoTracking().Where(o => o.ReservationId == reservationId)
        .Include(o => o.OrderItems)
        .ThenInclude(o => o.MenuItem)
        .SelectMany(order => order.OrderItems.Select(oi => oi.MenuItem))
        .ToListAsync();
    return menuItems;
}
```

## Lazy Loading

Lazy Loading defers the loading of related data until it is explicitly accessed. EF Core automatically loads the related entities when you first access a navigation property.

**How It Works?**

With lazy loading, EF Core doesn’t load related entities immediately. Instead, when you access a navigation property, a separate query is triggered to load the related data.

```csharp
var customer = dbContext.Customers.Find(1);
var orders = customer.Orders;
```

```csharp
protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
{
    optionsBuilder.UseLazyLoadingProxies();
}
```

## Explicit Loading

Explicit Loading is similar to lazy loading, but instead of automatically loading related entities, you manually request EF Core to load them using the Load() method. It gives you more control over when and how related data is loaded.

**How It Works?**

In explicit loading, EF Core does not automatically load related data when you access a navigation property. You explicitly tell EF Core to load the related data when needed.

```csharp
var customer = dbContext.Customers.Find(1);

dbContext.Entry(customer).Collection(c => c.Orders).Load();
```