# Generics

Generics in C# provide a powerful way to define classes, interfaces, methods, and delegates with a placeholder for the type of data they store or use. This allows you to write more flexible and reusable code that can operate on various data types while ensuring type safety at compile-time.

## Generic classes

Generic classes can be initialized like this.

Notice how generic type can also be passed as parameters and as a method type.

![image](https://github.com/user-attachments/assets/4782daad-2b5f-458d-9734-b4b87f1c7386)

Through the same class, we can declare a list of strings and integers.

![image](https://github.com/user-attachments/assets/38e4dbe2-5ffe-45d7-b3e2-ac109158ee50)

We can also have multiple parameters

```
class KeyValuePair<TKey, TValue>
{
    public TKey Key { get; set; }
    public TValue Value { get; set; }
}
```

## Generic Methods

- Methods that can work with any data type.
- The type parameter is specified when you call the method.

![image](https://github.com/user-attachments/assets/45595af8-a570-4ce4-9f0c-64b707e4d737)

![image](https://github.com/user-attachments/assets/a8258480-14bf-4c2b-b31e-73d6037085a6)

![image](https://github.com/user-attachments/assets/b8aec32a-3a15-4ddc-b17c-633c02dee41e)
