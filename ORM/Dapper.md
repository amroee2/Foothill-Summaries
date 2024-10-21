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

```chsarp
public async Task<int> DeleteEmployeeAsync(int employeeId)
{
    var sql = "DELETE FROM Employees WHERE EmployeeId = @EmployeeId";

    using (var connection = CreateConnection())
    {
        return await connection.ExecuteAsync(sql, new { EmployeeId = employeeId });
    }
}
```

