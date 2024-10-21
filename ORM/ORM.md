# ORM

Object-Relational Mapping (ORM) is a programming technique that allows developers to interact with a database using objects rather than writing SQL queries directly. ORM frameworks map database tables to classes, rows to objects, and columns to properties in an object-oriented programming language. This abstraction makes it easier to work with databases by allowing developers to manipulate data through familiar language constructs, reducing the need for manual SQL queries.

Key features of ORM include:

- Object-Database Mapping: ORM translates database tables and relationships into objects, attributes, and associations. Each database table corresponds to a class, and each row represents an instance of that class.

- CRUD Operations: ORMs simplify common database operations like Create, Read, Update, and Delete (CRUD) by generating SQL queries automatically, allowing developers to perform these actions with methods like Add, Find, Update, and Remove.

- Database Independence: ORMs abstract database-specific details, allowing developers to switch between different databases (e.g., SQL Server, PostgreSQL, MySQL) without changing the application's core logic.

- Relationships Handling: ORM frameworks handle relationships between tables, such as one-to-one, one-to-many, and many-to-many associations, mapping them to object relationships.

- Lazy and Eager Loading: ORM frameworks offer control over how related data is loaded. Lazy loading fetches related data only when it's accessed, while eager loading retrieves all necessary data in a single query.

- Migration Support: Many ORM frameworks support database schema migrations, enabling automatic updates to the database schema when models or data structures change.

## Example Class

```csharp

namespace RestaurantReservationCore.Db.DataModels
{
    public class Customer
    {
        public int CustomerId { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public string Email { get; set; }
        public string? PhoneNumber { get; set; }
        public List<Reservation> Reservations { get; set; }

        public Customer()
        {
            Reservations = new List<Reservation>();
        }

        public override string ToString()
        {
            return $"{CustomerId}, {FirstName}, {LastName}, {Email}, {PhoneNumber}";
        }
    }
}

```

Database

![image](https://github.com/user-attachments/assets/df942d02-2e43-4bd8-8aab-e34b447bd30d)


Code First Approach

In Code First approach, the focus is on the domain of the application by creating the classes rather than designing the database and then creating the matching classes. It is also called as Domain-Driven Design. All the database operations can be performed through the code and if there is any manual change on the database, it must be replicated on the code side as well otherwise the changes will be lost once the code updates the database.

Database First Approach

In Database First approach, the database designing is done first then the entity framework can attach with the database. If the database is already available, then the entity framework can be used to create (Plain Old CLR Object) POCO entities or model classes based on the database tables and columns, and the classes will be the bridge between the controller and the database. It is an alternative to the Code First approach where schema is available and entity framework will be used after that. In this case, the manual modifications will remain intact and will not be changed and the same must be apply to the application code.
