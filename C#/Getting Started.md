# Simple program

This is how a lot of C# simple programs start, it shares a lot of similarities with java.

From bottom up

- Console.WriteLine: Console is a class defined in the system namespace, its used mainly to write and read into/from the console, WriteLine is a **static method** (we can call it without making an instance of the console class).
- Main method: It's the first method run in the program, its **static** so we dont need to insnaniate from the Study class to run it, unlike java the main method doesnt have to be public, since it can invoke it from its assembly context.
- Classes: They are a main part of OOP, they represent the blueprint of class instances, talked about more in details later.
- Namespaces: Namespace is a block of code that can contain multiple classes, but its common convention to use one class per Namespace, they are used to distinct classes from each other if they have the same name, they can also contain other namespaces as well (nested namespaces).

![image](https://github.com/user-attachments/assets/0ccea3ba-5b35-4023-8709-1911a3faedc1)

The **using** lines above all "call" a certain class from the Namespace.

![image](https://github.com/user-attachments/assets/5a3d8184-5cb6-4b82-97e0-7f05b1bee1e3)

## Access modifiers

C# has four primary access modifiers: public, private, protected, and internal, each of which controls the visibility and accessibility of class members.

- Public: A public member can be accessed from anywhere in the code, meaning it is visible both within the class it is defined in and from any other class or assembly.
  
- Private: A private member is only accessible within the class where it is defined. It cannot be accessed from outside this class, including any derived classes.

- Protected: A protected member is accessible within its own class and by any derived class (subclass). It is not accessible from other classes that do not inherit from the base class.

- Internal: An internal member is accessible within the same assembly but not from outside the assembly. This is useful for restricting access to certain components while still allowing other parts of the same project to interact with them.

- Protected Internal: A combination of protected and internal, this access modifier allows the member to be accessed by derived classes and also by any class within the same assembly.

# Reference Type Vs Value Type 

## Value types

Value types are variables that contain the actual value, where the value is actually stored in a **stack**, when making a copy of a value type in an another value type, that copy is also stored in the same stack, so a change in one doesnt affect the other.

![image](https://github.com/user-attachments/assets/cb752849-f888-46b6-baf9-8976aae8f74a)

![image](https://github.com/user-attachments/assets/13733577-dbaa-4e45-8d58-89d27db41ea0)

Value types are like int, char, boolean, long....

## Reference types 

Reference types store a reference to a space in the **heap**, these types are also known as objects, when creating an object, the **object reference** is stored in the **stack**, while the actual values are stored in the **heap**.

Assume we have a person class.

![image](https://github.com/user-attachments/assets/e208ea8d-8b33-4304-bcbd-ec53e00fdd91)

And this program with the specified outputs.

At the beginning p1 and p2 references two different objects, and the references are stored in the stack while the actual values are in the heap. after setting p1 = p2, this modified p1 reference to equal p2 references in the stack, so now both point to the same exact heap in memory.

![image](https://github.com/user-attachments/assets/6d899d05-d881-409b-8a42-1b41651597a5)

# Program building blocks

In C#, program building blocks are the fundamental components used to construct applications. These building blocks allow developers to structure their code logically and effectively to implement functionality. Here are the primary building blocks in C#

Examples like 

- Namepaces
- Classes & Objects
- Methods
- Properities
- Fields
- Exception handling
- Enums
- Structs
- Control flow (if, else)
- Loops
- Interfaces

And anything else used to design a program/application in C#.

**Strings** are anamolies in C#, they are a reference type but considering that they are immutable objects, **a new object** is created that holds the new value, in this code for example, 3 objects are created, the original 2 and then a new one when assigning a new value to str1, "Amro" is still in the memory but will eventually get garbage collected.

![image](https://github.com/user-attachments/assets/92c3ca8a-66ca-4355-9e6c-4568ca384aa8)

# CTS

Common Type System (CTS) in C# ensures that all types share a common base and can be treated uniformly. This is achieved through a unified type system where all types, including value types like int, implicitly inherit from the System.Object class.

While value types are not reference types and do not extend System.Object in the traditional sense of inheritance, they are still implicitly derived from System.Object. This allows them to inherit basic functionalities like ToString(), GetHashCode(), and Equals().

To allow value types like int to be treated as objects, the .NET runtime provides a mechanism called boxing. Boxing wraps a value type in a reference type, allowing it to be used as an object. Once boxed, the value type behaves like any other reference type that derives from System.Object.

**Boxing**
```
int num = 123;
object obj = num; // Boxing: num is converted to an object
```
**Unboxing**
```
object obj = 123; // Boxing
int num = (int)obj;
```

## Type conversion

C# allows to convert types from one to another, thre are 3 ways this can be done:

- Implicit conversions: Done automatically, no special syntax, examples like converting from a smaller datatype to a larger one, and from derived classes (extending) to base classes (extended).

![image](https://github.com/user-attachments/assets/2f0c4a7f-5128-476d-8ddb-2c29544f5ec6)

- Explicit conversions (casting): Done through special syntax, opposite of Implicit conversions, when we convert from a larger type to a smaller one, and we ask the compiler to trust us and that we know this value can fit in a smaller datatype.

 ![image](https://github.com/user-attachments/assets/92624e1c-89c8-4566-b3ea-f06b8f8cf1a6)

![image](https://github.com/user-attachments/assets/f9eea940-1303-4e2e-ac6b-3642008555d1)

- Helper classes: They are classes that have static methods using to convert between primitives and references too. One class is the **Convert** class.

int num = 123;
string str = Convert.ToString(num);

string str = "123";
int num = Convert.ToInt32(str);

Also can be done using **methods**

int num = 123;
string str = num.ToString();

string str = "123";
int num = int.Parse(str);
