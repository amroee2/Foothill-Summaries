# Composite

The Composite design pattern is a structural pattern that allows you to treat individual objects and compositions of objects uniformly. It is commonly used to represent part-whole hierarchies, where individual objects and collections of objects are treated the same way. This is particularly useful when building tree structures like file systems, GUI components, or any object that contains nested structures.

Key Concepts of the Composite Pattern:
- Component: The abstract class or interface that defines common operations for both leaf and composite objects.
- Leaf: A class that represents individual objects, without any children.
- Composite: A class that represents a container (or parent) that can contain leaves or other composite objects.

If you have objects that are part of a hierarchy and some objects are collections of other objects, it can be difficult to handle these uniformly. The Composite pattern allows both individual objects (leaf) and groups of objects (composite) to be treated through a common interface, simplifying the client code.

Example: File System

FileSystem abstract cass is the commponent in this pattern, it defines the common operations that both the leaf and composite objects do (in this example, its the directory and file objects).
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Design_Patterns.Composite
{
    public abstract class FileSystem
    {
        public FileSystem(string name)
        {
            Name = name;
        }

        public string Name { get; }

        public abstract decimal GetKB();

        public abstract void Display(int depth);
    }
}
```

File directory represents the composite here, it had the add and remove operations, as well as a list of leaves (files).

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Design_Patterns.Composite
{
    public class FileDirectory : FileSystem
    {
        public FileDirectory(string name) : base(name)
        {

        }
        public List<FileSystem> Files { get; } = new List<FileSystem>();

        public override decimal GetKB()
        {
            return Files.Sum(f => f.GetKB());
        }

        public override void Display(int depth)
        {
            Console.WriteLine(new string('-', depth) + Name);
            foreach (var file in Files)
            {
                file.Display(depth + 2);
            }
        }
        public void Add(FileSystem file)
        {
            Files.Add(file);
        }
        public void Remove(FileSystem file) {
            Files.Remove(file);
        }
    }
}
```

FileItem class represents the leaves, the objects that have no children

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Design_Patterns.Composite
{
    public class FileItem : FileSystem
    {
        public decimal size { get; set; }
        public FileItem(string name, int size) : base(name)
        {
            this.size = size;
        }
        public override decimal GetKB()
        {
            return size;
        }
        public override void Display(int depth)
        {
            Console.WriteLine(new string('-', depth) + Name);
        }
    }
}
```
