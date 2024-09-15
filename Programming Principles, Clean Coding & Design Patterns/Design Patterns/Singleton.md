# Singleton

The Singleton design pattern ensures that a class has only one instance and provides a global point of access to it. This is particularly useful when you need a single object to coordinate actions across a system, such as a database connection, configuration manager, or logging service.

- Single instance: Ensures that only one instance of the class exists throughout the application.
- Global access point: Provides a static method that gives access to the single instance.

![image](https://github.com/user-attachments/assets/8883852b-517f-4122-971c-5c22a41780f4)

## Singleton structure

![image](https://github.com/user-attachments/assets/19d9dd8d-e894-44f4-9a2a-ff0f1a2e0a7e)

## Singleton features

![image](https://github.com/user-attachments/assets/c89d1968-e632-4b6e-9499-d8d0d5d7aece)

![image](https://github.com/user-attachments/assets/8f6052ed-d2e7-4417-a2d7-36da458e950d)

## Naive way

The naive way to implement the Singleton design pattern is to create the singleton without considering thread safety or lazy initialization. This implementation will work in simple, single-threaded applications but can lead to issues in multi-threaded environments.

```csharp

public sealed class Singleton
{
    private static Singleton _instance = null;

    private Singleton()
    {
    }

    public static Singleton Instance
    {
        get
        {
            if (_instance == null)
            {
                _instance = new Singleton();
            }

            return _instance;
        }
    }

    public void ShowMessage()
    {
        Console.WriteLine("Naive Singleton instance is working!");
    }
}

```

- Private Constructor: Prevents other classes from instantiating the class using the new keyword.
- Static Field _instance: Holds the reference to the single instance of the class.
- Instance Property: Checks if the instance is null before creating it. This ensures that the class is instantiated only once and reused afterward.
- Sealed class: prevents extending the class

The naive way is **not** thread safe, in a multi threaded enironment, it would be possible to create an instance **for each thread**

How it works:

assume we add these print statements 

```csharp
    private Singleton()
    {
        Console.WriteLine("Constructor invoked");
    }

    public static Singleton Instance
    {
        get
        {
            Console.WriteLine("Instance invoked");
            if (_instance == null)
            {
                _instance = new Singleton();
            }

            return _instance;
        }
    }
```

```csharp
Singleton instance = Singleton.Instance;
Singleton instance2 = Singleton.Instance;
Singleton instance3 = Singleton.Instance;
```

Output would look like this

![image](https://github.com/user-attachments/assets/235b7122-2b61-4af2-926f-a48ffe348d7e)

To make the class thread safe, we do this

```csharp
public class Singleton
{
    private static Singleton _instance = null;
    private static readonly object _lock = new object();

    private Singleton()
    {
        Console.WriteLine("Constructor invoked");
    }

    public static Singleton Instance
    {
        get
        {
            Console.WriteLine("Instance invoked");
            lock (_lock)
            {
                if (_instance == null)
                {
                    _instance = new Singleton();
                }
            }
            return _instance;
        }
    }
}
```

And the output will look the same.
