# Refactoring

Refactoring is simply the process of making a code cleaner, readable and understandable for us and other developers to be able to work with it in the future.

It goes hand in hand with clean coding principles, it is safe to say that applying clean coding principles after a code is written is called **refactoring**

![image](https://github.com/user-attachments/assets/94305357-2ea1-428c-81e6-34673042122a)

Like school assignments, we first make the first draft, then keep improving it until it reaches it's final version

![image](https://github.com/user-attachments/assets/7c6f0bd9-740f-42b0-b6ff-1cdfc9da3e0c)

## When to refactor?

- After writing unit tests: When we can validate that our current code design works correctly, we can go ahead and refactor, otherwise we might just be needing a new idea for the code and we would just be wasting our time.

- PDD: Pain driven development, refers to a code that is hard to maintain. When trying to introduce a new feature to an existing functionality, the said functionality will need refactoring if it's causing PDD.

- Bug Fixing: When identifying a bug and wanting to fix it, and then notice that refactored code would have prevented the bug from happening in the first place, go ahead and refactor.

- As a part of code review: Helps introduces only refactored code into the code base.

![image](https://github.com/user-attachments/assets/73df0365-989b-4780-a989-eee08c1d7405)

## When not

- Current code doesn't work: Similar to why we refactor after writing unit tests, if the current code doesn't work there is no point to refactor it, refactoring it might make it work, but its a rare occurnce.

- Massive technical debt: If the current system code has been ignoring clean code principles and have never been refactored, it sometimes might be best to create a new system with a similar functionalities from zero, and have it as lesson learned.

- Deadlines: If you have a very close deadline, and u wont have value of any refactoring until after the deadline, might be best to just do the refactor until after the deadline.

![image](https://github.com/user-attachments/assets/471aaae6-09b1-4bf8-aed9-48b9b225842c)

## Refactoring process

![image](https://github.com/user-attachments/assets/3869ba7d-d026-420b-8464-8ced6fbe7a8d)

![image](https://github.com/user-attachments/assets/a34b3f4d-f47e-4917-98e4-20d4554293da)

## Code smells

Code smells are indications that the code can benifit from refactoring.

![image](https://github.com/user-attachments/assets/5bcbc108-e861-42e7-bdfb-9d671ad8ed72)

## Principle of least astonishment

The Principle of Least Astonishment (POLA) states that software should behave in a way that minimizes surprises for users and developers. In other words, the behavior of a system should align with users' expectations based on their experience, context, or common sense.

- For Users: The user interface should behave as expected. Actions taken should lead to predictable results. For example, if a "Save" button unexpectedly deletes data, it would violate POLA because users wouldn't expect that behavior.

- For Developers: Code, APIs, and libraries should be intuitive and consistent. A method, for instance, should do exactly what its name suggests. If a method named getUser() returns data from a cache instead of fetching it from a database, it might cause confusion.

![image](https://github.com/user-attachments/assets/82e0272c-b74d-4dc9-a56e-55d0aef93707)

## Classification of code smells

- Bloaters

Bloaters are usually code constructs (methods, classes, or data structures) that have grown too large and become difficult to manage. It could be due to excessive parameters, large classes, or long methods. 

Example: Like a method that is excessively long, such as a function with 500 lines of code that tries to handle multiple responsibilities.

- Object Orientation Abusers

This occurs when object-oriented principles (e.g., inheritance, polymorphism) are used incorrectly or excessively, leading to poor design and maintenance issues.

Example: Misuse of inheritance, such as creating subclasses just for code reuse, even when the subclass does not fit the “is-a” relationship with the parent class.

- Changes preventers

This category refers to code that is difficult to modify or extend. Any change in one part of the system requires changes in several other places, leading to high coupling.

Example: Making a small change in the system requires multiple changes in different classes or methods. Like a class Order that directly depends on a class DatabaseConnection. If you need to switch to a new database system, you would have to modify the Order class directly.

- Dispensables

Dispensables are code elements that are unnecessary and can be safely removed, such as duplicate code, unused classes, or variables.

Example: Unused code or dead code, like a function that is never called anywhere in the program.

- Couplers

Couplers refer to code that has high interdependencies between components, making it difficult to reuse or refactor parts of the system independently.

Example: A class that knows too much about another class's internal details, violating the principle of encapsulation.

- Obfuscators

Obfuscators are code smells that make the code harder to read and understand. It could be due to unclear variable names, complex methods, or misleading comments.

Example: Poorly named variables or complex, unclear logic, like using int x1, x2, x3; without meaningful names.

![image](https://github.com/user-attachments/assets/91cb652e-dd68-439e-9171-1ec1ed0e1782)

# Statement Code Smells

These are code smells that occur on statement level (method calling, declaring variables...)

## Primitive Obsession 

Mentioned before in the Clean Coding principles in C# file, it refers to the overuse of primitive types instead of better abstractions or datastructures

![image](https://github.com/user-attachments/assets/a37f5c87-b894-4389-9d98-b411da30bdc7)

Example

**before**

![image](https://github.com/user-attachments/assets/54ee3e49-93b2-4824-bf94-31ea20b7b0cb)

**After**

![image](https://github.com/user-attachments/assets/a753a815-d5c7-4d66-b07a-368fe8f00235)

We can also replace temp variables with constants or enums (enum for months and another for days for example).

**Primitive obsession can result in a lot of duplicated code, so it's calssified as a bloater code smwell**

## Vertical Separation

Talked about in the Clean Coding principles in C# file as well, it's when variables are defined at the beginning of a method but only used much later, or when a method is called but the actual method is nowhere to be seen.

It's much better to declare variables **when they are needed**, and to make methods just **under the other method calling it** as much as possible.

![image](https://github.com/user-attachments/assets/7f788f41-1729-4011-b28c-5a2038a9163e)

**Vertical Sepearation can make code unnecessarily confusing, classifying it as an Obfuscator**

## Inconsistency

Not being consistent with the naming of variables, methods, classes or any declaration, or even indentations and patterns within the application.

Like not following conventions and excessive indentation 
![image](https://github.com/user-attachments/assets/f7beddda-cd43-4918-bc5a-6cad940cbfb7)

## Poor names

**Stick with conventions, avoid abbreviations and make sure its descriptive**
![image](https://github.com/user-attachments/assets/f641f351-f014-4b71-809e-358a4ec657da)

Before

![image](https://github.com/user-attachments/assets/60989346-e6fa-4a8a-82b8-59e1a36a00f7)

After

![image](https://github.com/user-attachments/assets/322fdbbb-f527-4d52-a742-de6f41e2870a)

Have some level of abstraction, assume here we are getting an order from a file, if somewhere in the code we decide to get it from an another source like an api, then our name here would simply be incorrect and **wrong**

Before

![image](https://github.com/user-attachments/assets/1acbc7e0-451e-4596-a15f-1ddf47db0a38)

After

![image](https://github.com/user-attachments/assets/fa843b87-a36f-4602-9531-c3a2d207b64a)

## Switch Statements

One or two switch statements are fine, but when they are used a lot in code, it would probably best to consider inheritance and polymorphism as an another approach.

![image](https://github.com/user-attachments/assets/46f12f19-3534-455f-a9e9-b9fc59ce1294)

![image](https://github.com/user-attachments/assets/c662bbc0-e6be-498a-98a9-1abd69ec8c0f)

## Dead code

This doesnt refer to commented out code, but code that exists in the codebase and can be called and used but they are not, they have no value and can just be safely deleted.

![image](https://github.com/user-attachments/assets/aac9b6d5-0108-4485-8dbe-d4df12ff326a)

## Hidden Temporal Coupling

It's when your class or program must follow a certain functionality for it to work correctly, but there is nothing that enforces such functionality.

![image](https://github.com/user-attachments/assets/aef5d486-3823-433f-97de-bc35038ff580)

Imagine if we have baked goods class, with these methods

We can simply call them in any order and it might cause problems with the code/logic

![image](https://github.com/user-attachments/assets/319153c5-d74d-449e-809a-6f949a9b72b8)

Better way to implement this is by having a method that encapsulates the other methods, and have all the inheriting children implement their own functionalities.

![image](https://github.com/user-attachments/assets/d061b4e5-e1c6-41e0-b002-6c2cd3820bb0)

# Method Code Smells

## Long Method
A method that has grown too large, doing too much work in one place. This makes it hard to understand, maintain, and reuse.

![image](https://github.com/user-attachments/assets/a727aaa8-02db-46e2-ae55-694a6a255c89)

![image](https://github.com/user-attachments/assets/068411db-b500-481b-9861-9145f7a73a65)

```
// Before (Long Method)
void ProcessOrder(Order order)
{
    ValidateOrder(order);
    CheckInventory(order);
    CalculateDiscounts(order);
    ApplyTaxes(order);
    // more logic...
}
```

## Obsucred Intent

The purpose of a method or piece of code is not immediately clear to someone reading it, often due to unclear naming or overly complex logic.

```
// Before (Obscured Intent)
void DoAction()
{
    if (x > 5 && y == 2) { /* logic */ }
}
```

## Conditional Complexity

Code with many conditionals (if/else or switch statements) becomes difficult to manage and test.

![image](https://github.com/user-attachments/assets/752c7a4b-987e-4088-a38a-7b44b4c16090)

![image](https://github.com/user-attachments/assets/ba73c7f9-8825-4c29-8772-aeadb5a607ec)

## Inconsistent Abstraction Level

A method mixes different levels of abstraction, e.g., combining high-level business logic with low-level implementation details.

![image](https://github.com/user-attachments/assets/175e9557-a468-406a-9a31-77c13e1c40f2)

```
// Before (Inconsistent Abstraction)
void PlaceOrder(Order order)
{
    // High-level
    SaveOrder(order);
    // Low-level
    string formattedDate = order.OrderDate.ToString("yyyy-MM-dd");
}
```

# Method Refactoring Techniques

## Extract Method <-> Inline Method

Extract Method: Moving part of a long method into a separate method to improve readability.

![image](https://github.com/user-attachments/assets/a4434b36-7b73-4dad-8298-cfb4981697eb)

Inline Method: Merging a method that is too simple and only called in one place back into the calling method.

![image](https://github.com/user-attachments/assets/149c5abd-deee-45d2-933b-cc11a3735155)

## Rename method

![image](https://github.com/user-attachments/assets/a8b5ff65-9213-42d2-9ca4-be4688b965ea)

```
// Before (Unclear Method Name)
void DoSomething()
{
    // logic
}

// After (Renamed Method)
void ValidateOrder()
{
    // logic
}
```

## Introduce Explaining Variable <-> Inline Temp:

![image](https://github.com/user-attachments/assets/988c92d1-4eeb-4031-a13b-c05d1978d3c4)

![image](https://github.com/user-attachments/assets/97f01345-81c2-4299-8add-20aabf3b2889)

```
// Before (Complex Expression)
if (order.Quantity * order.Price > 100) { /* logic */ }

// After (Explaining Variable)
bool isLargeOrder = order.Quantity * order.Price > 100;
if (isLargeOrder) { /* logic */ }
```

## Replace Temp with Query

Replacing temporary variables with method calls when the temporary variable is redundant.
 
![image](https://github.com/user-attachments/assets/8bca903f-4de6-4ec4-8bf8-86c37486ddc2)

```
// Before
int basePrice = order.CalculatePrice();
if (basePrice > 100) { /* logic */ }

// After
if (order.CalculatePrice() > 100) { /* logic */ }
```
