# NULL

The null is a unique data type which represents a value that is missing or does not exist.

NullReferenceException is thrown when there is an attempt to dereference a null object reference. A lot of effort has been put into preventing these exceptions.

The two fundamental data types in C# are value types and reference types. Value types cannot be assigned a null literal. The default value for reference types is null reference.

We can declare a type as **nullable** using the "?" near the type.
## Nullable value types

A nullable value type T? represents all values of its underlying value type T and an additional null value. For instance, the bool? variable can be assigned one of true, false, or null.

![image](https://github.com/user-attachments/assets/a66d38eb-90c9-448f-87b1-9163c6c0e784)

If the "?" to delcare that a value is nullable is not added, an error occurs and the program will not compile.

![image](https://github.com/user-attachments/assets/107e21f0-8641-4426-8738-a53c36bae53a)

We can also check if a value is null or not using simple if statements

![image](https://github.com/user-attachments/assets/91d2fed0-a069-47c1-9edd-377df9895c01)

Another way of checking if a value is null or not is using the HasValue attribute for nullables

![image](https://github.com/user-attachments/assets/4d0874ec-5947-4d12-a250-ae0e2d4cfea9)

## Null conditional operator

A null-conditional operator applies a member access, ?., or element access, ?[], operation to its operand only if that operand evaluates to non-null. If the operand evaluates to null, the result of applying the operator is null.

This would cause a null reference exception

![image](https://github.com/user-attachments/assets/5f2b0183-0b99-4801-b1ce-c0d35e5d85ae)

this wouldn't

![image](https://github.com/user-attachments/assets/96fb91aa-98ce-4d9a-9365-d4d523316740)

# ArgumentNullException

The ArgumentNullException is thrown when a null reference is passed to a method that does not accept it as a valid argument.

![image](https://github.com/user-attachments/assets/14980848-8c00-4795-a927-c589be80772b)

![image](https://github.com/user-attachments/assets/82dee6ba-5015-4e91-bade-fce38bda545a)

# Null-coalescing operator

Basically works like the if statement mentioned before.

It checks if the value is null, if it is, it will return whatever is after the "??" operator
![image](https://github.com/user-attachments/assets/7b24ec0e-2d23-4a68-be99-802df8ae0824)


# null-coalescing assignment operator

A lot similar to the one above, except it's used when assigning the value.

If initally the original value is not null, it will keep it.
![image](https://github.com/user-attachments/assets/ece002c0-e102-4a59-95c0-11c3d14a68f4)

![image](https://github.com/user-attachments/assets/dce77edb-6ec3-4109-82c2-d499dbb38af0)

But if it is null, it will take the new value assigned
![image](https://github.com/user-attachments/assets/82adb03e-92d7-4093-99d9-714e29554b91)

![image](https://github.com/user-attachments/assets/3f4ff6ac-f2c0-4e04-ae71-bbdf3251fe42)

# Reference types and Nullable context options

Null is a special value that represents the absence of an object. When a reference type variable is set to null, it doesn't point to any object in memory.

There are 4 options for the nullable context:

- Enabled

Reference types are treated as **non nullable** by default, which is why it issues a **warning**

![image](https://github.com/user-attachments/assets/eaacc605-f9bf-4cfb-8f41-50930015849b)

Using the nullable annotation **(?)**, the warning can be removed.

But it still shows that it may be null when doing operations on the value
![image](https://github.com/user-attachments/assets/e8eed0c7-967c-49f8-aacb-ce54ae26b776)

- Disabled

This makes reference types go back to before .NET6, where reference types where implicitly nullable, no warnings will show.

![image](https://github.com/user-attachments/assets/8c17a440-bda7-4d93-8d3b-8a6b8bbb8a38)

Adding the annotation would give this

![image](https://github.com/user-attachments/assets/33de8f6a-b8af-4685-b0fd-0f0fab9d932d)

- Warnings

Enables nullable reference type warnings but not annotations.

It will always show a warning when doing an operation
![image](https://github.com/user-attachments/assets/cfbd13d8-1663-4def-b499-8a8f09377318)

Adding the annotation would give this as well
![image](https://github.com/user-attachments/assets/a2b025fd-623b-40ed-936d-3a4ebb8e8e36)

- Annotations

The nullable notation will always be recognized, but it wont show warnings when doing an operation
![image](https://github.com/user-attachments/assets/3c5c71cf-f50c-455f-85e5-eb9697db893b)

# To add:

1- Null forgiving
2- The 9 null operations
