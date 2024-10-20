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
