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
