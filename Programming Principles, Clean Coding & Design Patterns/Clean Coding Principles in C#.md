# Clean Coding

clean coding is the task of making the code easier to:

- Read and Understand
- Maintain and Update
- Work with in the future

For the developer who wrote the code and the coworkers themselves.

3 Main principles to ensure that the code is clean:

![image](https://github.com/user-attachments/assets/bbf33c81-1093-4db2-abee-274ce7126b4d)

## Use the right tool

Using the right tool helps making the code more readable and understandable, and reduces the chances of bugs occuring as well.

When working with multiple tools like HTML, CSS, JS, C# and more, its important to use the right tool depending on the use case, and if possible, have only one tool per file.

This means to try as much as possible to not have multiple tools in the same file, inline css in HTML elements, or HTML formats in a SQL database, or inject JS code through C#....etc

![image](https://github.com/user-attachments/assets/7fcb0631-2bf3-40fd-bc8d-2ab03551df52)

Such actions would make a tool "potentially evil":

![image](https://github.com/user-attachments/assets/85d24649-5f5a-4cda-9205-94c6feacbede)

## High signal to noise ratio

It refers to how music have a high signal to noise ratio, making the noise not hearable in the background.

In coding, such signals are logic that follows the **TED** rule.

- Terse: Code should be concise and to the point, without unnecessary verbosity. This means avoiding redundant code and writing only what is needed to accomplish a task. Terse code is easier to read and understand because it eliminates noise.
  
- Expressive: Code should clearly communicate its purpose and functionality. This involves using meaningful variable and function names, as well as clear and straightforward logic. Expressive code allows developers to understand what the code does without needing to dig into documentation or comments extensively.

- Each function, method, or class should have a single responsibility. This principle aligns with the Single Responsibility Principle (SRP) in SOLID design (discussed in details later), where a piece of code should focus on one task or functionality. This makes the code more modular, easier to test, and simpler to maintain.

![image](https://github.com/user-attachments/assets/27bd5b01-4aab-4192-b101-d11632fc1905)

**Why is this so important?**

Its said that humans cant comprehend more than 7 items at a time, which is why we have the **Rule of 7**

![image](https://github.com/user-attachments/assets/7d89b4a2-8d47-4d56-973f-fbce117530fd)

Dirty code tends to build up, when we use long methods within other long methods for example, or have a class do a lot of things, it'll be harder in the future after writing thousands of lines of code to refactor the program, which is why we have to **refactor regularly**.

![image](https://github.com/user-attachments/assets/7a7ba12a-0b84-4364-b62b-0b382a3c9586)

another important principle here is to avoid repetition, or **DRY (Dont Repeat Yourself)**.

### DRY

DRY stands for Don't Repeat Yourself. It is a fundamental principle in software development that encourages the reduction of repetition in code.

![image](https://github.com/user-attachments/assets/9c964e05-4c51-4bb9-bd27-f77045b2cc6a)

Example on DRY

```
//NOT DRY
public class AreaCalculator
{
    public double CalculateRectangleArea(double length, double width)
    {
        return length * width;
    }

    public double CalculateSquareArea(double side)
    {
        return side * side;
    }
}
```

```
//DRY
public class AreaCalculator
{
    public double CalculateArea(double dimension1, double dimension2 = 0)
    {
        return dimension2 == 0 ? dimension1 * dimension1 : dimension1 * dimension2;
    }
}
```

Normally when we have a repeated pattern in code, it means that there is repetition in the code that can be reduced.

## Self documenting

Self-documented code is code that is written in such a way that its purpose and functionality are clear from the code itself, without needing additional comments or external documentation.

It refers to the way we can write the code in a way it can express itself (readable and understandable), without the need of comments, which can be done by having clear naming for namespaces, classes, methods, fields or any other programming block.

## Naming

As mentioned before, having a clear name makes the code much more readable and understandable.

### Naming Classes

Class names must be specific, directly to the point and follow single responsibility principle.

Avoid confusing names, abbreviations, or have one class do multiple tasks (violating SRP).

![image](https://github.com/user-attachments/assets/03be72bc-735b-4a6a-b8d5-df95895e08a1)

Strive for making classes **cohesive**, as in have its method work with each other, a non cohesive class is a class that has a lot of methods that work independently.

![image](https://github.com/user-attachments/assets/07dea942-47f1-436d-bfc8-0ec88b96f273)

### Naming methods

When naming a method, we should select one that clearly describes the functionality of the method.

![image](https://github.com/user-attachments/assets/4e0b5efd-103b-4de5-a0cb-0bc024536fae)

Using words like "and", "or" or "if" probably means that our method is doing multiple functionalities at the same time, and its a sign that we should just divide it into two methods.

**DO NOT INCLUDE SIDE EFFECTS**

When a method is named "GetUser", it should just get the user details for example, it should not create a new session for the said user.

### Naming booleans

When naming boolean variables, we should strive for the name to be **conditional** and **symmetric**, having two words that are the direct opposite of each other makes the code much more readable

![image](https://github.com/user-attachments/assets/45fe4855-3c23-40a9-aeb4-55c61c526df1)

![image](https://github.com/user-attachments/assets/0b6fa917-8484-4020-8213-ef9f118c36e3)

# Clean Conditionals 

Clean written conditionals clearly convey intent, and cleary describe why should we go "left or right"

## Compare booleans implicitly 

if(loggedIn == true) adds unnecessary code, when talking with someone we dont ask them if them logging in is true, we ask if they logged in.

![image](https://github.com/user-attachments/assets/cb4bd07f-3f21-4147-895d-6aa462f2c873)

## Assign booleans implicitly 

Same logic above applies here.

![image](https://github.com/user-attachments/assets/2f9f2a41-bdbd-447b-b5e8-e167262f024d)

Strive to make your code reads like speech as much as possible.

## Be Positive

Writing complex boolean names can cause a lot of confusion and unnecessary complexity.

![image](https://github.com/user-attachments/assets/de04ab96-a014-489d-bc23-64002ae6a742)

Use positive conditionals.

## Ternary Operations

**When to use ternary?**

When the logic is simple and doesnt require a whole if else statements.

![image](https://github.com/user-attachments/assets/042d6116-327e-4684-a2e5-6dd349eb14a2)

**Do not overuse ternaries**, avoid using nested ternary operations, or when the conditional statement is large.

## Be strongly typed

Advantages:

- No Typos: if we make a spelling mistake, the IDE will catch it, while if we make a mistake in the string manager here we will only catch the mistake when a logical error happens.
- Intellisense: the IDE will help with writing the operation
- Document states: Through this enum, we can know that there are finite number of EmployeeType, which can help understand the code workflow
- Searchable: Manager option can be easily find when searching for it (through references), but when searching for a string u will find it in multiple places (comments, different use cases...etc).

![image](https://github.com/user-attachments/assets/0d6d764d-51d7-4ec0-9781-713c2db9f826)

## Avoid magic numbers

Write them in expressive constants

![image](https://github.com/user-attachments/assets/4435795b-1d50-48e6-be02-571fd3e0cd3f)

And use enums with types/options

![image](https://github.com/user-attachments/assets/207c966f-29e1-4159-a9c3-0c63a7a36a42)

## Complex Conditionals

Use intermediate variables to know the answer of what the conditional is asking.

![image](https://github.com/user-attachments/assets/60f36c90-8087-44bd-aec9-415e32624763)

We can also encapsulate complex conditionals within methods and have the method name to be the answer.

![image](https://github.com/user-attachments/assets/be0cb51d-7f92-4be5-99d5-814904410dd4)

## Polymorphism over Enums

Try to utilize polymorphism over enums when possible, instead of having all the type within the enum, we can create different type of classes and have one common one as an abstract class

![image](https://github.com/user-attachments/assets/16cee641-39ce-4970-adb5-98921d7384d1)

And then we can use the shared method/operation intended for the enum, just through one line of code (here its user.login), utilizing Run time polymorphism (method overriding).

![image](https://github.com/user-attachments/assets/ecbab297-66af-4a49-9b56-92de29c258bd)

## Be Declarative

Dont write code to do an operation when there are already an existing one that can do it, less likely to have a bug + fewer lines of code.

Example using LINQ.

![image](https://github.com/user-attachments/assets/5ffe60cd-20a3-4777-b368-c0f44bba71b7)

## Sometimes code is not the answer

When there are a lot of hardcoded values within an operation, and those hardcoded values are likely to change in the future, it is better to store them in a table instead of using switch statements to handle them.

- Easier to change
- Much fewer lines of code

![image](https://github.com/user-attachments/assets/9cd38305-bcd3-48f2-86d4-c1ee5a9033e0)
