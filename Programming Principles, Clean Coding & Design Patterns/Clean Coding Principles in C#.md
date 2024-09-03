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


# Clean Methods

When to create a function/method

- Duplication: When you see a lot of repeated patterns/duplication, its a sigh that a method can be used to simplify code
- Indentation: When the code is too much indented (arrow shaped), its a sign to create method within these conditionals
- Unclear intent: We can use functions with expressive name to express our intentions
- More than one task: When the current block of code does more than one task, its a clean sign to use methods

![image](https://github.com/user-attachments/assets/bc8a9d25-954a-4629-94b6-18e40965e3c3)

## Duplication

Repeated patterns like this can be refactored into methods

![image](https://github.com/user-attachments/assets/89c9ab50-4f8a-4be3-8685-154c6ca70683)

## Excessive indentation

The more the code is shaped as an arrow, the excessive the indentation

![image](https://github.com/user-attachments/assets/616a0e4b-b3c4-415f-b218-2cdce868cbc5)

**Solutions for excessive indentation**

- Extract Method
- Fail Fast
- Return Early

![image](https://github.com/user-attachments/assets/76c115f5-c573-4835-bf09-fc3ea238a709)

### Extract Method

![image](https://github.com/user-attachments/assets/0b612970-755f-4cba-b52b-d4bcbae908aa)

### Fail Fast

![image](https://github.com/user-attachments/assets/b3972749-1f5d-4a42-952a-e83f2e45a3cc)

### Return Early

Before

![image](https://github.com/user-attachments/assets/1ff7fd25-aca2-4b8d-80fd-be3fd5eff9eb)

After

![image](https://github.com/user-attachments/assets/b522dbd2-64e5-48fa-9713-c06e279f25ff)

## Convey intent

Use method name to convey intentions

![image](https://github.com/user-attachments/assets/9fa8d257-71c8-4f21-988c-423cda116e20)

## Do One Thing

Methods are like paragraphs in books, they are needed to make the book more readable and easy to understand, and they describe **one thing**

![image](https://github.com/user-attachments/assets/017dd4c8-fea5-417c-bd06-2a7fcf68020d)

## MayFly Variables

MayFly flies are flies that dont live for long, 30m - 24h lifespan.

We can apply the same logic for variables within methods, create a variable only when its needed.

When writing a method that does only one task, the thread will swiftly execute it and use the variables, so with such methods you automatically end up with having MayFly variables.

![image](https://github.com/user-attachments/assets/313d1662-a220-446c-badc-f1cafbad79d2)

## How many paramters?

![image](https://github.com/user-attachments/assets/6f6c61f9-4a87-4843-bf7e-9550909e680b)

Strive to have a few number of variables, having multiple ones can be a sign of a method doing more than one task, also avoid flag arguments as they are unneeded, you can specify the course of an action before calling the method.

![image](https://github.com/user-attachments/assets/b3fd5e1c-6d7c-4335-b149-62efc99bafd2)

![image](https://github.com/user-attachments/assets/00e9194e-c360-4b53-bbc8-078d8a78f88d)

## Signs a method is too long

- White Space and Comments: If a method has a lot of them, to the point it seperates a lot of lines of codes and needs comments to convey intent (not self documenting code), it means that the method can benifit form being split up.
- Scrolling required
- Naming issues: If we are struggling to name the method, it might be a sign it does more than one task, and hence need to be split up
- Multiple Conditionals: As we saw before in arrow shaped block of code, splitting it into multiple methods makes it more readable
- Hard to digest: If a method complexity is high and its hard to understand, its a sign that splitting it into multiple methods can make it more expressive (self documenting)

**Remember the rule of 7**

![image](https://github.com/user-attachments/assets/4bf23420-12c4-451a-8a2a-9df6198017a6)

# Clean Classes

Classes are like headings in books, the heading name gives a general overview about what the paragraphs will talk about, same can be applied to classs names and its methods

**When to create a class?**
![image](https://github.com/user-attachments/assets/119aed4c-cfee-438a-893d-f36e5b05194c)

## Cohesion

A class methods must be able to worth together and use each other to achieve high cohesion, having a lot of methods that dont work together in the same class can be a sign that new classes being created can be helpful.

![image](https://github.com/user-attachments/assets/941b4989-9f68-40bf-9218-e1e603c706d9)

## Primitive obsession

When trying to apply a method on a class, there is no need to pass all parameters like this, it makes the code much less readable, we can instead simply pass on the reference to the object.

![image](https://github.com/user-attachments/assets/6e1b29bc-4b95-4e34-a389-dd0cf893ec4c)

## Proximity principle

This is a loose role, but try to make a method that calls another next to each other, since we typically read from top to bottom.

![image](https://github.com/user-attachments/assets/07f599ca-b5aa-4b12-a6b5-ad12a1ae03bd)
