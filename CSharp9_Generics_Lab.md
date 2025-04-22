
# C# 9 Generics — Complete Lab with File Structure and Explanations

This hands-on lab covers all topics from the Pluralsight course *C# 9 Generics* by Thomas Claudius Huber. It is designed to reinforce key concepts through practice, with clear file paths and theoretical explanations.

---

## ✅ Prerequisites

- .NET 5.0 SDK or later
- Visual Studio 2019/2022 or Visual Studio Code
- Basic C# knowledge (classes, interfaces, inheritance, methods)

---

## 📦 Module 1: Understanding the Need for Generics

### 🔹 Concept

Without generics, you must choose between duplicating code or using `object` (which removes type safety and may hurt performance). Generics allow you to write reusable, type-safe, performant code.

### 📁 `WiredBrainCoffee.StackApp/SimpleStack.cs`

```csharp
public class SimpleStack
{
    private readonly double[] _items = new double[10];
    private int _currentIndex = -1;

    public void Push(double item) => _items[++_currentIndex] = item;
    public double Pop() => _items[_currentIndex--];
    public int Count => _currentIndex + 1;
}
```

### 📁 `WiredBrainCoffee.StackApp/Program.cs`

```csharp
var stack = new SimpleStack();
stack.Push(1.2);
stack.Push(2.8);
stack.Push(3.0);

double sum = 0.0;
while (stack.Count > 0)
{
    var item = stack.Pop();
    Console.WriteLine($"Item: {item}");
    sum += item;
}
Console.WriteLine($"Sum: {sum}");
```

---

## 📦 Module 2: Implementing Generic Classes

### 🔹 Concept

Generic classes allow you to create type-safe containers or services that can operate on any data type.

### 📁 `WiredBrainCoffee.StorageApp/Entities/IEntity.cs`

```csharp
public interface IEntity
{
    int Id { get; set; }
}
```

### 📁 `WiredBrainCoffee.StorageApp/Entities/Employee.cs`

```csharp
public class Employee : IEntity
{
    public int Id { get; set; }
    public string? FirstName { get; set; }
    public override string ToString() => $"{Id}: {FirstName}";
}
```

### 📁 `WiredBrainCoffee.StorageApp/Repositories/GenericRepository.cs`

```csharp
public class GenericRepository<T> where T : IEntity
{
    private readonly List<T> _items = new();

    public void Add(T item) { item.Id = _items.Count + 1; _items.Add(item); }
    public T GetById(int id) => _items.Single(i => i.Id == id);
    public void Remove(T item) => _items.Remove(item);
    public void Save() => _items.ForEach(Console.WriteLine);
}
```

---

## 📦 Module 3: Working with Generic Interfaces

### 🔹 Concept

Generic interfaces allow you to decouple the definition of operations from the data type. You can switch from a list-based implementation to a database-based one without changing the consuming code.

### 📁 `WiredBrainCoffee.StorageApp/Repositories/IReadRepository.cs`

```csharp
public interface IReadRepository<out T>
{
    IEnumerable<T> GetAll();
    T GetById(int id);
}
```

### 📁 `WiredBrainCoffee.StorageApp/Repositories/IWriteRepository.cs`

```csharp
public interface IWriteRepository<in T>
{
    void Add(T item);
    void Remove(T item);
    void Save();
}
```

### 📁 `WiredBrainCoffee.StorageApp/Repositories/IRepository.cs`

```csharp
public interface IRepository<T> : IReadRepository<T>, IWriteRepository<T>
    where T : IEntity
{}
```

---

### 📁 `WiredBrainCoffee.StorageApp/Program.cs`

```csharp
// Usando ListRepository con interfaces genéricas
IWriteRepository<Employee> employeeRepo = new ListRepository<Employee>();
employeeRepo.Add(new Employee { FirstName = "Julia" });
employeeRepo.Add(new Employee { FirstName = "Anna" });
employeeRepo.Save();

IReadRepository<Employee> readRepo = (IReadRepository<Employee>)employeeRepo;
foreach (var employee in readRepo.GetAll())
{
    Console.WriteLine($"Read: {employee.FirstName}");
}
```

## 📦 Module 4: Creating Generic Methods and Delegates

### 🔹 Concept

Generic methods allow you to reuse logic across different types. Delegates allow you to define methods as parameters. Combined with generics, they give you powerful abstraction tools.

### 📁 `WiredBrainCoffee.StorageApp/Repositories/RepositoryExtensions.cs`

```csharp
public static class RepositoryExtensions
{
    public static void AddBatch<T>(this IWriteRepository<T> repo, T[] items)
    {
        foreach (var item in items) repo.Add(item);
        repo.Save();
    }
}
```

### 📁 `WiredBrainCoffee.StorageApp/Entities/EntityExtensions.cs`

```csharp
public static class EntityExtensions
{
    public static T? Copy<T>(this T item) where T : IEntity
    {
        var json = JsonSerializer.Serialize(item);
        return JsonSerializer.Deserialize<T>(json);
    }
}
```

### 📁 `WiredBrainCoffee.StorageApp/Program.cs` (excerpt)

```csharp
employeeRepository.AddBatch(new[] { new Employee { FirstName = "Sara" } });
```

---

## 📦 Module 5: Special Cases with Generics

### 🔹 Concept

Static members in generic classes are type-specific. You can also hide class type parameters in method declarations. Operator overloading with generics requires dynamic or special patterns.

### 📁 `WiredBrainCoffee.SpecialCases/Container.cs`

```csharp
public class Container<T>
{
    public static int InstanceCount { get; private set; }
    public Container() => InstanceCount++;
}
```

### 📁 `WiredBrainCoffee.SpecialCases/Program.cs`

```csharp
_ = new Container<string>();
_ = new Container<int>();
Console.WriteLine(Container<string>.InstanceCount); // 1
Console.WriteLine(Container<int>.InstanceCount);    // 1
```

---

## 📚 Summary

- ✅ Covered: Generic classes, interfaces, methods, delegates, constraints, events, static members, and edge cases.
- 🧠 Reinforced type safety, reuse, and performance via generics.
- 📂 All code organized per module with file paths for easy reference.
