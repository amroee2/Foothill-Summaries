# Reflection

Reflection in C# is a powerful feature that allows you to inspect metadata about types, methods, properties, and other members of a class at runtime. It can be used to dynamically create instances of types, invoke methods, or access fields and properties.

Reflection in C# is able to perform operations such as inspecting types, invoking methods, and accessing properties because it works with the metadata stored in a compiled assembly file.

```
using System;
using System.Reflection;

public class Example
{
    public void ShowMessage()
    {
        Console.WriteLine("Hello from ShowMessage method!");
    }
}

public class Program
{
    public static void Main()
    {
        // Load the current executing assembly
        Assembly assembly = Assembly.GetExecutingAssembly();

        // Get the type information of the 'Example' class from the assembly
        Type exampleType = assembly.GetType("Example");

        // Create an instance of the 'Example' class
        object exampleInstance = Activator.CreateInstance(exampleType);

        // Get the MethodInfo object representing the 'ShowMessage' method
        MethodInfo showMessageMethod = exampleType.GetMethod("ShowMessage");

        // Invoke the 'ShowMessage' method on the instance of 'Example'
        showMessageMethod.Invoke(exampleInstance, null);
    }
}
```

## Creating instances of a class using constructors

Assume this person class

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ReflectionSample
{
    public class Person
    {
        public string Name { get; set; }
        private int Id { get; set; }

        public int age;
        public Person()
        {
            Console.WriteLine("New person was created");
        }
        public Person(string name)
        {
            Name = name;
            Console.WriteLine($"New person with name {Name} was created");

        }
        private Person(int id, string name)
        {
            Id = id;
            Name = name;
            Console.WriteLine($"New person with name {Name} and Id {Id} was created");

        }

        public void Talk( string message)
        {
            Console.WriteLine(message);
        }
        private void Yell(string message)
        {
            Console.WriteLine(message.ToUpper());
        }
        public override string ToString()
        {
            return $"Name: {Name}, Id: {Id} age: {age}\n";
        }
    }
}
```

As always, we can create instances of a class using its constructors, which we can get through **.GetConstructors** from Reflection namespace.

We can also utilize **binding flags**, which are used to specify what exactly we want from the data members depending on if we used get constructors, get properties or the other common class members.

- BindingFlags.Instance specifies that only instance members (members that are associated with an instance of a type) should be included in the search.
- BindingFlags.NonPublic: Members that are not public in the class
- BindingFlags.Public: Members that are public

![image](https://github.com/user-attachments/assets/8ca97595-25a8-431a-80a6-b07681202866)

Then we can use the invoke method to create instances dynamically.
![image](https://github.com/user-attachments/assets/1feaff2c-a4ed-41de-95ed-2ea63beca98e)

It's also possible to use the **Activator** class in the System namespace that is used to create classes dynamically at runtime.

![image](https://github.com/user-attachments/assets/eec73ac0-8004-4a6c-b3fd-1f37061b64e9)

It can also be used with private members.

```
var person6 = Activator.CreateInstance(
    "ReflectionSample", // The name of the assembly where the type is located
    "ReflectionSample.Person", // The fully qualified name of the type
    true, // Indicates whether to ignore case when matching the type name
    BindingFlags.Instance | BindingFlags.NonPublic | BindingFlags.Public, // Specifies which constructors are used to find a match
    null, // Specifies the binder to use, or null for the default binder
    new object[] { 1, "Kevin" }, // An array of arguments to pass to the constructor
    null, // Culture-specific information, or null for the current culture
    null // Activation attributes, or null if not applicable
)?.Unwrap();
```
CreateInstance returns an ObjectHandle, which is a wrapper that allows you to interact with an object across different application domains. Unwrap() returns the actual object from the ObjectHandle.

As mentioned before, we can also access properties and fields.

![image](https://github.com/user-attachments/assets/2d415db9-0912-4795-9bb7-8a9c17331200)

And it is also possible to invoke methods.

```

var talkMethod = person6?.GetType().GetMethod("Talk");
talkMethod?.Invoke(person6, new[] {"Something to say"} );

person6?.GetType().InvokeMember("Yell", BindingFlags.Instance | BindingFlags.InvokeMethod | BindingFlags.NonPublic, null, person6, new[] {"Something to say"} );
```

