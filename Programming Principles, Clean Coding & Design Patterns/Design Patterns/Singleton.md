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

## Using static constructor and neted class

```csharp
public sealed class Singleton
{
    private Singleton()
    {
        Console.WriteLine("Constructor invoked");
    }

    private static class SingletonHolder
    {
        // Static constructor ensures that the instance is created only when accessed
        internal static readonly Singleton instance = new Singleton();
    }

    public static Singleton Instance
    {
        get
        {
            Console.WriteLine("Instance invoked");
            // The instance is created only when this is called for the first time
            return SingletonHolder.instance;
        }
    }

    public void ShowMessage()
    {
        Console.WriteLine("Singleton with static constructor and nested class is working!");
    }
}

```
Why Use a Nested Class?
- Lazy Initialization: The SingletonHolder class is only loaded into memory when the Instance property is accessed for the first time. This is a form of lazy initialization.
- Thread Safety: Static constructors in C# are automatically thread-safe, so the Singleton instance is guaranteed to be created safely, even in a multi-threaded environment.
- No Locking Overhead: Because C# handles static initialization in a thread-safe way, there's no need to use manual locking (lock) to ensure that only one instance is created. This improves performance.

## Lazy <T>

The Lazy<T> class in C# is a built-in way to ensure lazy initialization and thread safety without the need for manual locks or static constructors. It's a highly recommended approach for creating Singleton instances.

```csharp
public sealed class Singleton
{
    private static readonly Lazy<Singleton> _lazyInstance = new Lazy<Singleton>(() => new Singleton());

    private Singleton()
    {
    }

    public static Singleton Instance
    {
        get
        {
            return _lazyInstance.Value;
        }
    }

    public void ShowMessage()
    {
        Console.WriteLine("Lazy<T> Singleton instance is working!");
    }
}
```

- Lazy<T>: The Lazy<T> class is designed to handle lazy initialization and thread safety. It creates the Singleton instance only when the Value property is accessed for the first time.
- Thread Safety: By default, Lazy<T> provides thread safety (LazyThreadSafetyMode.ExecutionAndPublication), ensuring that only one thread can initialize the Singleton instance.
- No Manual Locks or Nested Class: You don't need a nested class, static constructor, or explicit locking mechanisms. Lazy<T> handles all of this internally, making the code simpler and more efficient.

Lazy<T> Is the most common approach when working with singleton.

Singelton vs Static classes

![image](https://github.com/user-attachments/assets/90999ee4-0629-4bf5-ac60-0c65d00671de)
