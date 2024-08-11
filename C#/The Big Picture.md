# C#

C# Is an object oriented programming language that is a mixture of both Java and the C Family.

OOP came out in 2001 after the Rivarly between CPP and Java, and solved a lot of issues that where in both languages.

**What makes C# a good programmling language?**

![image](https://github.com/user-attachments/assets/670b65cd-5f4c-49b1-ae08-fc61829f80f5)

## Approachable 

C# Has a lot of similar syntax to CPP and Java, it uses semiconlons, curly braces, zero indexed and supports object oriented concepts like namespaces, classes, methods and properties.

![image](https://github.com/user-attachments/assets/886e1719-1414-4b27-a53a-da59cfbe9005)

## Strongly typed 

Like c plus plus and java, C# requires the developer to state the data type of variables/parameters they declare either primitive (int, double, float, char, long...) or reference types like class instances, arrays, interfaces...

C# also allows to use **var** to declare a value, and then uses **inference** to find out the datatype of the declared value in compile time.

![image](https://github.com/user-attachments/assets/c0f0f70e-f842-4b34-8088-a543eb399678)

![image](https://github.com/user-attachments/assets/12dbbef6-67b4-4b9f-a5da-5a90da73f380)

## Resilient and Safe

### Safety

C# Also has exceptions, which are events the distrub the normal workflow of the program.

For eaxmple, if an index out of bound happens (I.E access an index equal or larger than the array length) in cpp, it's highly likely to cause a memory corruption, while in C# and Java it would raise a **runtime exception**

![image](https://github.com/user-attachments/assets/eb2cc65f-afdd-4f57-9935-df4f6cd8e208)

### Resilient
Assume we have this point class, where we can simply add X and Y coords.

![image](https://github.com/user-attachments/assets/7c9c34c8-12cc-444e-9e11-38782ffcd52e)
![image](https://github.com/user-attachments/assets/0734e71a-c31d-4aa4-b4a4-535f5a7237f8)

Assuming this point class is a part of a package/library for example, if the point class is changed and deployed to include X,Y,Z coords, this **will not** break our main file, it would just add a default value for the Z coords, this is one example of how C# is **resilient to change**

![image](https://github.com/user-attachments/assets/5d24eb5c-4498-4c90-9a46-c46ea35bee43)

## Object Oriented 

C#, as previously mentioned, supports object oriented programming with all OOP pillars (Encapsulation, Abstraction, Inheritance, Polymorphism).

It also has functional features, or pre-defined methods for the classes like arrays.

For example, instead of finding the sum of integers in an array like this:

![image](https://github.com/user-attachments/assets/4d998aa5-3ff6-4bb3-ba2d-fe1839005979)

We can use this:

![image](https://github.com/user-attachments/assets/b4dee1f6-5178-4a86-b4ee-cdb000ca0c33)

## Open Source & Cross Platform, General Purpose

- Open Source & Cross Platform: C# Is currently an open source project, its also used to develop console and web apps on windows, mac and other operating systems.
- General Purpose: C# Is used to develop multiple applications/programs, including mobile and web applications, games and more.

# Code execution models

C# Is a **managed** language model, it lies between compiled languages like CPP and interperted ones like Python.

It has strong typing from compiled languages but it also has an automatic memory management as well, unlike CPP.
![image](https://github.com/user-attachments/assets/f8c26a78-f75e-4cee-a7b6-4a64815f269d)

C# compilation happens by first converting the code into intermediate language (Assembly file), which is then passed to a part of an execuion engine called JIT (Just in time), this engine only converts code reached in the program into machine code, meaning if a function is never called, JIT **never** wastes it resources on it.

Moreover, through the JIT engine, if a method is called 1000 times, the 1st time it gets converted from assembly to machine code (in run time) then the cpu executes it, but in all the other 999 times, the cpu can just execute it directly from the machine code.

![image](https://github.com/user-attachments/assets/bf5752db-4639-4681-97ac-3ea79096ed1a)

# CLR Engine

![image](https://github.com/user-attachments/assets/3ee11b6d-a001-44fe-8b69-11a39abef59d)

Common language runtime is the engine responsible of handling the .net family compilation, it contains the JIT we talked about, garbage collection and runtime type safety (like exceptions).

The "CL" part in "CLR" refers to how all .net languages like C#, F# and VB can have a different high level syntax but the **same** intermediate language, meaning that we could use a method wrote in F# from another file in a C# file, and it would run without issues.
