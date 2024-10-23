# Dapper

Dapper is a lightweight, high-performance micro-ORM (Object-Relational Mapper) for .NET, designed to map data between a relational database and C# objects. It's an alternative to Entity Framework (EF) when performance, simplicity, and control over SQL queries are required.

Dapper is a micro-ORM, meaning it focuses on simplifying database interaction without abstracting away SQL queries. It doesn’t manage entity states, relationships, or migrations.


![image](https://github.com/user-attachments/assets/66e1e3e3-be8d-48cb-bcf5-434f5fcca5c0)

How Dapper Works
 
“Dapper Majorly Include Three Steps”
 
Step 1
Create an IDBConnection object with Connection String.

```csharp
static IDbConnection db = new SqlConnection(ConfigurationManager.ConnectionStrings["SqlServerConnString"].ConnectionString);  
```
 
Step 2
Write a query and store it in a normal string variable.

 ```csharp
String query = "select * from contacts";  
```

Step 3
Call db.Query() and pass the query and it's done.

```csharp
(List<Contact>)db.Query<Contact>(query);  
```

## Inserting into DB

```csharp
public async Task<int> AddEmployeeAsync(Employee employee)
{
    var sql = @"INSERT INTO Employees (FirstName, LastName, Email) 
                VALUES (@FirstName, @LastName, @Email)";
                
    using (var connection = CreateConnection())
    {
        return await connection.ExecuteAsync(sql, new
        {
            employee.FirstName,
            employee.LastName,
            employee.Email
        });
    }
}
```

## Reading

```csharp
public async Task<IEnumerable<Employee>> GetAllEmployeesAsync()
{
    var sql = "SELECT EmployeeId, FirstName, LastName, Email FROM Employees";

    using (var connection = CreateConnection())
    {
        return await connection.QueryAsync<Employee>(sql);
    }
}

public async Task<Employee> GetEmployeeByIdAsync(int employeeId)
{
    var sql = "SELECT EmployeeId, FirstName, LastName, Email FROM Employees WHERE EmployeeId = @EmployeeId";

    using (var connection = CreateConnection())
    {
        return await connection.QueryFirstOrDefaultAsync<Employee>(sql, new { EmployeeId = employeeId });
    }
}

```

## Update 

```csharp
public async Task<int> UpdateEmployeeAsync(Employee employee)
{
    var sql = @"UPDATE Employees 
                SET FirstName = @FirstName, 
                    LastName = @LastName, 
                    Email = @Email 
                WHERE EmployeeId = @EmployeeId";
    
    using (var connection = CreateConnection())
    {
        return await connection.ExecuteAsync(sql, new
        {
            employee.FirstName,
            employee.LastName,
            employee.Email,
            employee.EmployeeId
        });
    }
}
```

## Delete

```csharp
public async Task<int> DeleteEmployeeAsync(int employeeId)
{
    var sql = "DELETE FROM Employees WHERE EmployeeId = @EmployeeId";

    using (var connection = CreateConnection())
    {
        return await connection.ExecuteAsync(sql, new { EmployeeId = employeeId });
    }
}
```

 # Dapper vs EF Core

## Dapper

**Speed**: Dapper is known for being extremely fast, often touted as the "King of Micro ORMs." because it executes raw SQL queries directly.

**Ease of use**: Dapper is easy to work with for developers that are comfortable with SQL, as it only executes raw sql queries.

**Manual Mapping**: Dapper requires more manual work when handling complex relationships, joins, and nested objects.

**Flexibility**: It is lightweight and flexible, but the absence of built-in features like change tracking can make maintaining large-scale applications more difficult.

**Features**: 

- Minimalistic: Dapper is focused on speed and simplicity. It provides simple object mapping and does not support advanced ORM features like relationships, change tracking, or migrations.

- Limited Features: It’s mainly used for SELECT queries and executing raw SQL. Anything beyond simple object mapping (like handling complex relationships) requires manual SQL.

## EF Core

- Speed: EF Core is generally slower than Dapper because it is a full-featured ORM that abstracts database interactions, meaning it doesn't execute raw SQL directly unless explicitly configured to. This additional abstraction adds overhead, but EF Core has been optimized in recent versions to reduce the performance gap.

- Ease of use: EF Core is easier for developers who prefer working with objects rather than writing raw SQL. It offers a high level of abstraction, making it more beginner-friendly for those unfamiliar with SQL.

- Automatic Mapping: EF Core automatically maps relationships, joins, and complex object graphs between tables and classes, which reduces manual work but can add complexity if not carefully managed.

- Flexibility: While EF Core provides a lot of flexibility in terms of querying, the abstraction layer can sometimes limit how efficiently developers can write optimized SQL queries. However, developers can always fall back on raw SQL using methods like FromSqlRaw.

**Features**:

- Change Tracking: EF Core includes built-in change tracking, which allows developers to modify entities and have EF automatically generate the correct SQL commands to update the database.

- Migrations: EF Core supports database migrations, which help in managing schema changes over time. This is a key feature for applications that need to evolve their database structure.

- Relationships: EF Core has strong support for managing relationships (one-to-many, many-to-many) between entities through navigation properties, including lazy, eager, and explicit loading options.

- LINQ: EF Core uses LINQ to allow developers to write database queries in C#, which are translated into SQL queries by the ORM. This makes code more readable and easier to maintain.
