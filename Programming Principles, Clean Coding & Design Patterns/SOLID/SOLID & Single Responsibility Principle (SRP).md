# Solid Principles

The SOLID principles are a set of five design principles that help software developers create more maintainable, scalable, and understandable systems. They form a framework for building robust and adaptable object-oriented code. The SOLID acronym stands for:

- Single Responsibility Principle (SRP)
- Open/Closed Principle (OCP)
- Liskov Substitution Principle (LSP)
- Interface Segregation Principle (ISP)
- Dependency Inversion Principle (DIP)

# Single Responsibilty Principle (SRP)

SRP states that a class should have only one reason to change, meaning it should only have one responsibility or focus. By adhering to SRP, you make the code easier to maintain and modify because changes to one responsibility won't affect the others. This principle helps avoid tightly coupled classes that try to do too many things at once.

A class following SRP would be responsible for only one part of the functionality of an application, and if there is a need to change that class, the change will affect only that single responsibility.

Benefits:

- Maintainability: Easier to update, refactor, and understand.
- Testability: Easier to write unit tests because each class has a specific purpose.
- Flexibility: Helps to separate concerns, making the system more flexible for future change

Example:

Assume we have this invoice class

```csharp
public class Invoice {

    private Book book;
    private int quantity;
    private double discountRate;
    private double taxRate;
    private double total;

    public Invoice(Book book, int quantity, double discountRate, double taxRate) {
        this.book = book;
        this.quantity = quantity;
        this.discountRate = discountRate;
        this.taxRate = taxRate;
        this.total = this.calculateTotal();
    }

    public double calculateTotal() {
            double price = ((book.price - book.price * discountRate) * this.quantity);

        double priceWithTaxes = price * (1 + taxRate);

        return priceWithTaxes;
    }

    public void printInvoice() {
            System.out.println(quantity + "x " + book.name + " " +          book.price + "$");
            System.out.println("Discount Rate: " + discountRate);
            System.out.println("Tax Rate: " + taxRate);
            System.out.println("Total: " + total);
    }

        public void saveToFile(String filename) {
    // Creates a file with given name and writes the invoice
    }

}
```

It violates SRP.

It has multiple reasons to change, maybe we want to change how we calculate the total, or how to print the invoice, or if to save to a file or a database.

Implement new classes to avoid this:


```csharp
public class InvoicePrinter {
    private Invoice invoice;

    public InvoicePrinter(Invoice invoice) {
        this.invoice = invoice;
    }

    public void print() {
        System.out.println(invoice.quantity + "x " + invoice.book.name + " " + invoice.book.price + " $");
        System.out.println("Discount Rate: " + invoice.discountRate);
        System.out.println("Tax Rate: " + invoice.taxRate);
        System.out.println("Total: " + invoice.total + " $");
    }
}
```

```csharp
public class InvoicePersistence {
    Invoice invoice;

    public InvoicePersistence(Invoice invoice) {
        this.invoice = invoice;
    }

    public void saveToFile(String filename) {
        // Creates a file with given name and writes the invoice
    }
}
```

The Original Class Breakdown:

The Invoice class in the example you shared handles multiple responsibilities:

- Business logic (calculateTotal): Calculating the total price based on discounts and tax rates.
- Output logic (printInvoice): Handling the printing of the invoice.
- Persistence logic (saveToFile): Saving the invoice to a file.

To apply SRP:

- Business Logic (calculateTotal): Calculating the total is core to the Invoice class and is tightly bound to the attributes of Invoice. This logic depends on the invoice’s specific details (like the book, quantity, discountRate, etc.). Therefore, it's appropriate to keep calculateTotal in the Invoice class because it's part of its primary responsibility.

- Output Logic (printInvoice): Printing the invoice is not related to calculating or holding invoice data. It involves formatting and displaying information, which could change (e.g., different print formats). Therefore, it's a separate concern that should be moved into a class specifically responsible for output operations, such as a InvoicePrinter or InvoiceFormatter.

- Persistence Logic (saveToFile): Similarly, saving to a file is about storing the invoice, which is also a different concern. Changes to file formats or storage methods would affect this, so it should be moved to a class dedicated to saving, like an InvoiceRepository or InvoiceSaver.

Now we have three classes

- Invoice
- InvoicePrinter
- InvoicePersistence

Each with one reason to change.

Another example

Before

```csharp

using System;
using System.Collections.Generic;

class Employee
{
    public string Name { get; set; }
    public int Age { get; set; }

    public void SaveEmployeeDetails(Employee employee)
    {
        // Code to save employee details to a database
        Console.WriteLine("Employee details saved.");
    }

    public void GenerateEmployeeReport(Employee employee)
    {
        // Code to generate a report of the employee
        Console.WriteLine("Employee report generated.");
    }
}

class Program
{
    static void Main(string[] args)
    {
        Employee employee = new Employee { Name = "John", Age = 30 };
        employee.SaveEmployeeDetails(employee);
        employee.GenerateEmployeeReport(employee);
    }
}
```

After

```csharp
using SOLID;

class Program
{
    static void Main(string[] args)
    {
        Employee employee = new Employee { Name = "John", Age = 30 };
        EmployeeDetails.SaveEmployeeDetails(employee);
        EmployeeReport.GenerateEmployeeReport(employee);
    }
}
```
```csharp
namespace SOLID
{
    public class Employee
    {
        public string Name { get; set; }
        public int Age { get; set; }
    }
}
namespace SOLID
{
    public class EmployeeDetails
    {

        public static void SaveEmployeeDetails(Employee employee)
        {
            Console.WriteLine("Employee details saved.");
        }
    }
}
namespace SOLID
{
    public class EmployeeReport
    {
        public static void GenerateEmployeeReport(Employee employee)
        {
            Console.WriteLine("Employee report generated.");
        }
    }
}
```

We kept Employee class on its own because its primary concern is holding data, if it had a **simple** work method for example, like:

```csharp
public class Employee {
    public string Name { get; set; }
    public int Age { get; set; }

    public void Work() {
        Console.WriteLine($"{Name} is working.");
    }
}

```

We can keep the work method in the Employee class.

**SRP is a principle, not a rule**

We have to decide when we should apply SRP and have different classes, its not always about having one method per class, we can have multiple ones and it would still follow SRP, like this InvoiceCalculator that it's primary concern is to find invoice total:

```csharp
public class InvoiceCalculator
{
    private double discountRate;
    private double taxRate;

    public InvoiceCalculator(double discountRate, double taxRate)
    {
        this.discountRate = discountRate;
        this.taxRate = taxRate;
    }

    public double CalculateDiscountedPrice(double originalPrice)
    {
        return originalPrice - (originalPrice * discountRate);
    }

    public double CalculateTaxAmount(double price)
    {
        return price * taxRate;
    }

    public double CalculateFinalPrice(double originalPrice, int quantity)
    {
        double discountedPrice = CalculateDiscountedPrice(originalPrice);
        double totalPrice = discountedPrice * quantity;
        double taxAmount = CalculateTaxAmount(totalPrice);

        return totalPrice + taxAmount;
    }
}

```

As a general rule of thumb, if you have to scroll further down to see more methods you have, then its either one of the two:

- You have long methods and need to apply refactoring techniques (talked about previously)
- Its time to divide methods into different classes
