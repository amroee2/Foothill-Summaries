# LINQ

Language intergrated query is a sql-like syntax for C# and other visual basic languages.

LINQ provides a consistent query syntax that works across various data sources such as in-memory collections (like arrays, lists), XML documents, databases, and more. LINQ brings the capabilities of querying databases to the C# language syntax itself, making it easy to filter, sort, and manipulate data. 

There are two main styles for writing LINQ queries in C#:

- Query Syntax: Similar to SQL and typically more readable for complex queries.
- Method Syntax: Uses method calls and lambda expressions, providing more flexibility and is often more concise.

```
List<int> numbers = new List<int> { 1, 2, 3, 4, 5, 6 };

// Query Syntax
var evenNumbersQuery = from number in numbers
                       where number % 2 == 0
                       select number;

// Method Syntax
var evenNumbersMethod = numbers.Where(number => number % 2 == 0);

foreach (var num in evenNumbersQuery)
{
    Console.WriteLine(num);  // Output: 2, 4, 6
}
```
It can be used for searching, ordering, aggrevate functions (sum, min, max...) and other common operations.

# Select and Order

## Select all

![image](https://github.com/user-attachments/assets/ade836f6-29ea-4bc0-84bf-c41e850887c1)

## Select one column

![image](https://github.com/user-attachments/assets/ee477508-34a5-452a-badf-ebc13216d424)

## Select specific columns

![image](https://github.com/user-attachments/assets/da0ac1a2-6386-4df6-8e1c-190a79576497)

## Order by ascending

![image](https://github.com/user-attachments/assets/c0b0e47c-04c8-4bbb-a841-662b9d8a4b81)

## Order by descending

![image](https://github.com/user-attachments/assets/b795a605-347c-4bae-bd61-3c07a0e4e4f4)

## Order by multiple columns

![image](https://github.com/user-attachments/assets/0e0da81a-c0e2-49ee-927a-9625d56a0adb)

# Where and filtering

## Where

![image](https://github.com/user-attachments/assets/029b7527-c5bf-4b12-960d-8610d4c593ea)

## Where Starts With

![image](https://github.com/user-attachments/assets/9f343691-63dd-4add-b36d-f416aded2ab9)

## Multiple conditions

![image](https://github.com/user-attachments/assets/a43d77f7-2113-4b2e-b5b2-5f667f2e34cd)

## First and First or default

![image](https://github.com/user-attachments/assets/7d179dd2-c7b9-4e59-a31f-ea5fc55b243c)

## Last and last or default

![image](https://github.com/user-attachments/assets/d8328caf-439d-4c7e-a788-e893e6919e9f)

## Single and single or default

![image](https://github.com/user-attachments/assets/0960f2ce-c1f2-45c1-b9a3-0db080d3e09e)

# Assigning and Partitioning

## Assigning property
![image](https://github.com/user-attachments/assets/e18166a4-8db1-40ca-b8ec-0e5b43c0dd19)

## Take and take while

![image](https://github.com/user-attachments/assets/d0796ee2-debd-4b15-b692-b07a5dab65a7)

## Skip and skip while

![image](https://github.com/user-attachments/assets/b93cbe35-864f-49b7-a24a-d28556bff1b9)

## Distinct 

![image](https://github.com/user-attachments/assets/783b9897-5bfb-4666-bb84-e697d5801b31)

# Data in collections

## Any

![image](https://github.com/user-attachments/assets/9437b28d-4840-4039-95e7-ba6588cc0e88)

## All

![image](https://github.com/user-attachments/assets/99bbef77-c95c-40ae-b4fa-67348adf36ad)

## Contains for int, double, float (value types)

![image](https://github.com/user-attachments/assets/e3fd1dd1-8325-4b13-9025-710142a14c65)

## Contains for reference types

![image](https://github.com/user-attachments/assets/fecadea8-4461-44f5-9195-6f87edb4de6c)

![image](https://github.com/user-attachments/assets/fe04755a-9ec0-47f7-bff8-2a62a5d40c76)

# Compare and union collections

## Sequence Equals

![image](https://github.com/user-attachments/assets/ab467bf4-c9cb-41e7-9ef9-6e290c4b43cc)

![image](https://github.com/user-attachments/assets/d0b4b445-bb82-46a2-942e-69db219bafa6)

## Except

![image](https://github.com/user-attachments/assets/9a8db4fc-e05a-4059-a5bd-780fad3590d6)

## Intersect

![image](https://github.com/user-attachments/assets/388647cb-7f53-4dde-a1d6-5f2ae8742aaa)

## Union

![image](https://github.com/user-attachments/assets/faffa1cf-a081-4f45-b53f-c165a9eed484)

## Concat

![image](https://github.com/user-attachments/assets/9757b594-ec9e-4a29-950e-0204739b7bef)

![Uploading image.png…]()
