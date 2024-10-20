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
