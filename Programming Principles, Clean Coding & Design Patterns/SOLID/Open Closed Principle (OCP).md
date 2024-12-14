# Open/Closed Principle

The Open/Closed Principle (OCP) is the second principle in SOLID, and it states:

Software entities (like classes, modules, functions) should be open for extension but closed for modification.

This means that the behavior of a class should be extendable without modifying its existing code. OCP encourages developers to write code that can adapt to new requirements by **adding new code**, not by changing existing code.

Why OCP Is Important:
- Minimizes Changes: Once a class is tested and used in production, modifying it can introduce bugs or require extensive retesting. OCP helps reduce the need to alter existing, stable code.
- Increases Flexibility: OCP allows for new functionality to be added by extending the current implementation (usually via inheritance, composition, or interfaces), making the system more flexible and scalable.

How to Implement OCP:
- Use inheritance to extend functionality.
- Use interfaces or abstract classes to allow the system to be extended by adding new types that conform to the interface, without modifying the original implementation.

Remember our Invoice class from SRP file, after we updated the class to implement single responsibilty principle, we ended up with some new classes, with one of them being the InvoicePersistence class.

Assume now we add functionality to save into a database:

```csharp
public class InvoicePersistence {
    Invoice invoice;

    public InvoicePersistence(Invoice invoice) {
        this.invoice = invoice;
    }

    public void saveToFile(String filename) {
        // Creates a file with given name and writes the invoice
    }

    public void saveToDatabase() {
        // Saves the invoice to database
    }
}
```
Another way to implement saveToDatabase method is by using **interfaces**

We can convert InvoicePersistance to an interface:

```csharp
interface InvoicePersistence {

    void save(Invoice invoice);
}

```

Then add 2 new classes, one to implement save to file and the other for database

```csharp
public class DatabasePersistence : InvoicePersistence {

    public void save(Invoice invoice) {
        // Save to DB
    }
}
public class FilePersistence : InvoicePersistence {

    public void save(Invoice invoice) {
        // Save to file
    }
}
```

Now our persistence logic is easily extendable. If our boss asks us to add another database and have 2 different types of databases like MySQL and MongoDB, we can easily do that.

Now, when needed to save into a certain system, we can utilize **polymorphism**.

We can now pass any class that implements the InvoicePersistence interface to this class with the help of polymorphism. This is the flexibility that interfaces provide.

```csharp
public class PersistenceManager {
    InvoicePersistence invoicePersistence;
    BookPersistence bookPersistence;

    public PersistenceManager(InvoicePersistence invoicePersistence,
                              BookPersistence bookPersistence) {
        this.invoicePersistence = invoicePersistence;
        this.bookPersistence = bookPersistence;
    }
}
```
