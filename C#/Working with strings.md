# ToLower, ToUpper and ToTitleCase

![image](https://github.com/user-attachments/assets/88426375-f6a8-49e0-999b-0e7ab0e32866)

# Appending Strings 

![image](https://github.com/user-attachments/assets/aba9af77-1a4a-4e30-b24d-e75c7c62599c)

# StringBuilder

The StringBuilder class is mutable. When you append, insert, or modify a string using StringBuilder, it modifies the internal buffer rather than creating new strings. This makes StringBuilder much more efficient for scenarios where you're frequently modifying strings.

![image](https://github.com/user-attachments/assets/6f541084-ab3b-4bfc-9c6f-6825013e6ef2)

![image](https://github.com/user-attachments/assets/947cb4ae-a5b1-4446-bbfe-5ed700e316f7)

# Concat, Join and Split

![image](https://github.com/user-attachments/assets/56fecac9-ef19-42c8-917d-7da6c8530726)

![image](https://github.com/user-attachments/assets/cd6053f1-dd4a-46c9-81f6-330ab885d7f2)

# Trim and Pad

![image](https://github.com/user-attachments/assets/741972d4-5656-4519-a32d-b5ec77ece183)

![image](https://github.com/user-attachments/assets/b34e0d78-03db-4f91-b924-f7fdc0433fe7)

# Starts with, End with and Contains

![image](https://github.com/user-attachments/assets/901223ea-55ee-436e-a9a7-8620e86751a6)

# IndexOf and LastIndexOf

![image](https://github.com/user-attachments/assets/7c802e4b-c3ea-4a56-b930-927a5f72d651)

# Compare, CompareTo and Equal

```
int result = string.Compare("apple", "banana");

if (result == 0)
{
    Console.WriteLine("Strings are equal.");
}
else if (result < 0)
{
    Console.WriteLine("First string is less than second."); // output
}
else
{
    Console.WriteLine("First string is greater than second.");
}
```
```
string str1 = "apple";
string str2 = "banana";

int result = str1.CompareTo(str2);

if (result == 0)
{
    Console.WriteLine("Strings are equal.");
}
else if (result < 0)
{
    Console.WriteLine("First string is less than second.");
}
else
{
    Console.WriteLine("First string is greater than second.");
}
```
```
string str1 = "apple";
string str2 = "apple";

bool isEqual = str1.Equals(str2);

if (isEqual)
{
    Console.WriteLine("Strings are equal.");
}
else
{
    Console.WriteLine("Strings are not equal.");
}
```
# Substring, replace, insert, remove

```
string str = "Hello, World!";
string subStr1 = str.Substring(7);        // Extracts from index 7 to the end
string subStr2 = str.Substring(0, 5);     // Extracts the first 5 characters

Console.WriteLine(subStr1);  // Output: "World!"
Console.WriteLine(subStr2);  // Output: "Hello"
```

```
string str = "Hello, World!";
string replacedStr1 = str.Replace('o', 'a');      // Replaces 'o' with 'a'
string replacedStr2 = str.Replace("World", "C#"); // Replaces "World" with "C#"

Console.WriteLine(replacedStr1);  // Output: "Hella, Warld!"
Console.WriteLine(replacedStr2);  // Output: "Hello, C#!"
```
```
string str = "Hello, World!";
string insertedStr = str.Insert(7, "Beautiful ");  // Inserts "Beautiful " at index 7

Console.WriteLine(insertedStr);  // Output: "Hello, Beautiful World!"
```
```
string str = "Hello, World!";
string removedStr1 = str.Remove(5);           // Removes from index 5 to the end
string removedStr2 = str.Remove(7, 5);        // Removes 5 characters starting from index 7

Console.WriteLine(removedStr1);  // Output: "Hello"
Console.WriteLine(removedStr2);  // Output: "Hello, !"
```
