# Collections

In C#, collections are used to store, manage, and manipulate groups of related objects. The .NET framework provides a variety of collection types, each designed to handle specific scenarios.

# Non-Generic collections

Non-generic collections were introduced in early versions of .NET and are found in the System.Collections namespace. They store elements as objects (object type), meaning they can hold any type of data. 

- They are not type safe, we would need to cast them to be able to work with the element inside.
- Relies on Boxing-Unboxing, which can impact performance

**Arraylists**
```
ArrayList list = new ArrayList();
list.Add(1);
list.Add("Hello");
int num = (int)list[0];  // Requires casting
```

**Hashtable**

```
Hashtable table = new Hashtable();
table.Add(1, "One");
string value = (string)table[1];  // Requires casting
```

And others, notice how in nowhere the type of the elements is specified.

# Generic collections

Generic collections, introduced in .NET 2.0 and found in the System.Collections.Generic namespace, provide type safety and better performance. They are strongly typed, meaning they only accept a specified data type, eliminating the need for casting and reducing the risk of runtime errors.

- Type safe since we specify the element we want to hold.
- No boxing/unboxing = better performance

**list**

```
List<int> list = new List<int>();
list.Add(1);
int num = list[0];  // No casting needed
```
**Dictionary**

```
Dictionary<int, string> dict = new Dictionary<int, string>();
dict.Add(1, "One");
string value = dict[1];  // No casting needed
```

Each collection has built in method to be able to add, remove and manipulate data within it.

Arraylist methods for example

```
ArrayList list = new ArrayList();
list.Add(1); // Adds 1 to the list
list.Insert(0, "Hello"); //Inserts Hello at the specified index
list.remove(1); // Removes the first occurnce of 1
list.RemoveAt(0); // Removes object at index 0
list.Clear(); // Removes all elements
```
