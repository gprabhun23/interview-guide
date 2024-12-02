**1. What are Property Accessors in C#?**  
- Property accessors allow controlled access to class properties.  
- They use `get` and `set` keywords for reading and modifying property values.  
- You can implement logic inside accessors for validation or other operations.  
- *Example*:  
  ```csharp  
  public class Person  
  {  
      private int age;  
      public int Age  
      {  
          get { return age; }  
          set { if (value > 0) age = value; }  
      }  
  }  
  // Applied in my project to validate user inputs for age.
  ```

**2. What is an Object in C#?**  
- An object is an instance of a class that encapsulates data and methods.  
- It is created using the `new` keyword.  
- Objects allow interaction with data defined in classes.  
- *Example*:  
  ```csharp  
  Person person = new Person();  
  person.Age = 30;  
  Console.WriteLine(person.Age);  
  // Used objects to manage student data in my education portal project.
  ```

**3. What is the difference between `continue` and `break` statements in C#?**  
- `continue` skips the current iteration of a loop and moves to the next.  
- `break` exits the loop immediately.  
- Both improve control flow in looping structures.  
- *Example*:  
  ```csharp  
  for (int i = 0; i < 5; i++)  
  {  
      if (i == 2) continue;  
      if (i == 4) break;  
      Console.WriteLine(i);  
  }  
  // Utilized these in a task scheduler to manage incomplete tasks.
  ```

**4. What is C#?**  
- C# is a modern, object-oriented programming language developed by Microsoft.  
- It runs on the .NET platform and supports cross-platform development.  
- Features include type safety, garbage collection, and LINQ support.  
- *Example*:  
  ```csharp  
  Console.WriteLine("Hello, World!");  
  // Used C# to build APIs for microservices architecture in my cloud solutions project.
  ```

**5. What do you understand by Value types and Reference types in .NET? Provide some comparison.**  
- Value types store data directly, while reference types store references to data.  
- Value types include `int`, `float`, and `struct`, whereas reference types include `class` and `string`.  
- Value types are stored in the stack, reference types in the heap.  
- *Example*:  
  ```csharp  
  int a = 5;  
  string b = "Hello";  
  // Differentiated storage requirements in a high-performance computation project.
  ```

**6. What are Generics in C#?**  
- Generics allow defining reusable classes or methods with type parameters.  
- They increase code reusability and type safety.  
- Examples include `List<T>` and `Dictionary<TKey, TValue>`.  
- *Example*:  
  ```csharp  
  public void PrintItems<T>(List<T> items)  
  {  
      foreach (var item in items)  
          Console.WriteLine(item);  
  }  
  // Used generics to handle collections in a data processing library.
  ```

**7. How is Exception Handling implemented in C#?**  
- Exception handling uses `try`, `catch`, and `finally` blocks.  
- `try` encapsulates code that may throw exceptions.  
- `catch` handles specific exceptions, and `finally` executes cleanup code.  
- *Example*:  
  ```csharp  
  try { int x = int.Parse("abc"); }  
  catch (FormatException ex) { Console.WriteLine(ex.Message); }  
  finally { Console.WriteLine("Done"); }  
  // Applied in my project to handle file I/O errors gracefully.
  ```

**8. Why use the `finally` block in C#?**  
- The `finally` block ensures the execution of cleanup code regardless of exceptions.  
- It is optional but recommended for resource management.  
- Commonly used for releasing resources like file streams or database connections.  
- *Example*:  
  ```csharp  
  StreamReader sr = null;  
  try { sr = new StreamReader("file.txt"); }  
  finally { sr?.Dispose(); }  
  // Implemented in a logging utility to handle resource management.
  ```

**9. What are partial classes in C#?**  
- Partial classes allow splitting a class definition into multiple files.  
- All parts are combined into a single class during compilation.  
- Useful for managing large classes and auto-generated code.  
- *Example*:  
  ```csharp  
  // File1.cs  
  public partial class Demo { public void Method1() { } }  
  // File2.cs  
  public partial class Demo { public void Method2() { } }  
  // Utilized in an ASP.NET Core project to separate logic and UI code.
  ```

**10. Can `this` be used within a static method in C#?**  
- No, `this` refers to the instance of a class and is inaccessible in static methods.  
- Static methods are bound to the class, not the instance.  
- Use the class name directly in static methods instead.  
- *Example*:  
  ```csharp  
  public static void PrintClassName() { Console.WriteLine(typeof(MyClass).Name); }  
  // Applied in my project for utility methods.
  ```

**11. Can multiple `catch` blocks be executed?**  
- No, only the first matching `catch` block executes for a single exception.  
- Further `catch` blocks are ignored.  
- Ensure specific exceptions are caught before general ones.  
- *Example*:  
  ```csharp  
  try { int x = int.Parse("abc"); }  
  catch (FormatException) { Console.WriteLine("Format issue."); }  
  catch (Exception) { Console.WriteLine("General exception."); }  
  // Handled various exception types in a payment gateway project.
  ```

**12. What is Serialization in C#?**  
- Serialization converts objects into a format (like JSON or XML) for storage or transmission.  
- Deserialization reconstructs objects from the serialized format.  
- Commonly used for saving application state or transferring data.  
- *Example*:  
  ```csharp  
  string json = JsonSerializer.Serialize(obj);  
  var obj = JsonSerializer.Deserialize<MyClass>(json);  
  // Used serialization in API communication for data exchange.
  ```

**13. What are the different types of classes in C#?**  
- `Static` classes: For utility methods and no instances.  
- `Abstract` classes: Provide base functionality for derived classes.  
- `Sealed` classes: Prevent inheritance.  
- *Example*:  
  ```csharp  
  public static class Utils { public static void Print() { } }  
  // Implemented static classes for reusable utility functions.
  ```

**14. What is Managed or Unmanaged Code in C#?**  
- Managed code runs under the control of the CLR, ensuring memory safety.  
- Unmanaged code executes directly on the OS without CLR oversight.  
- Managed code benefits from features like garbage collection.  
- *Example*:  
  ```csharp  
  // Managed  
  string text = "Hello";  
  // Used unmanaged code through P/Invoke in a native library integration project.
  ```

**15. What are Reference Types in C#?**  
- Reference types store memory addresses, not the actual data.  
- Examples include `class`, `interface`, and `string`.  
- They allow sharing of the same data across multiple references.  
- *Example*:  
  ```csharp  
  string s1 = "Hello";  
  string s2 = s1;  
  // Managed references in a caching mechanism for performance optimization.
  ```
  **16. What is LINQ in C#?**  
- LINQ (Language-Integrated Query) is used to query data collections like arrays, lists, or databases.  
- It provides a unified syntax for querying various data sources.  
- Commonly used LINQ methods include `Select`, `Where`, `OrderBy`, and `GroupBy`.  
- *Example*:  
  ```csharp  
  var numbers = new List<int> { 1, 2, 3, 4 };  
  var evenNumbers = numbers.Where(n => n % 2 == 0);  
  // Utilized LINQ to filter and process data in a reporting module.
  ```

**17. What is the difference between `string` and `StringBuilder` in C#?**  
- `string` is immutable; every modification creates a new instance.  
- `StringBuilder` is mutable and optimized for frequent modifications.  
- Use `string` for static or fewer changes; use `StringBuilder` for dynamic content.  
- *Example*:  
  ```csharp  
  StringBuilder sb = new StringBuilder("Hello");  
  sb.Append(" World");  
  Console.WriteLine(sb.ToString());  
  // Applied `StringBuilder` to dynamically generate large HTML strings.
  ```

**18. What is Boxing and Unboxing in C#?**  
- Boxing converts a value type to a reference type by wrapping it in an object.  
- Unboxing extracts the value type from the boxed object.  
- Both operations affect performance due to type conversion overhead.  
- *Example*:  
  ```csharp  
  int num = 10;  
  object obj = num;  // Boxing  
  int newNum = (int)obj;  // Unboxing  
  // Managed type conversions efficiently in a generic computation engine.
  ```

**19. What is the difference between a class and a structure in C#?**  
- A class is a reference type; a structure is a value type.  
- Classes support inheritance; structures do not.  
- Classes are stored on the heap, while structures are stored on the stack.  
- *Example*:  
  ```csharp  
  public struct Point { public int X, Y; }  
  public class Shape { public int Width, Height; }  
  // Chose structures to represent lightweight coordinate data in a graphics application.
  ```

**20. What is the difference between a Struct and a Class in C#?**  
- Structs are value types, whereas classes are reference types.  
- Structs do not support inheritance, while classes do.  
- Structs are better for lightweight objects; classes for complex types.  
- *Example*:  
  ```csharp  
  struct Employee { public int Id; }  
  class Department { public string Name; }  
  // Used structs for fixed, small data elements in a scientific computation app.
  ```

**21. What is an Abstract Class in C#?**  
- An abstract class provides a base for other classes but cannot be instantiated.  
- It may contain abstract methods (without implementation) and concrete methods.  
- Abstract classes enforce derived classes to implement certain functionality.  
- *Example*:  
  ```csharp  
  public abstract class Animal { public abstract void Speak(); }  
  public class Dog : Animal { public override void Speak() => Console.WriteLine("Bark"); }  
  // Designed abstract classes for consistent behavior across animal types in a simulation.
  ```

**22. What is a namespace in C#?**  
- A namespace organizes code into a logical structure to prevent naming conflicts.  
- It is declared using the `namespace` keyword.  
- Namespaces can be nested and are commonly used in large projects.  
- *Example*:  
  ```csharp  
  namespace MyApp.Models { public class User { public string Name; } }  
  // Used namespaces to organize models, services, and utilities in a web application.
  ```

**23. What are Nullable types in C#?**  
- Nullable types allow value types to hold `null`.  
- They are declared using `?`, e.g., `int?`.  
- Useful for representing the absence of a value, such as in databases.  
- *Example*:  
  ```csharp  
  int? age = null;  
  Console.WriteLine(age.HasValue ? age.Value : "No Age");  
  // Managed nullable fields in a customer record system to represent optional data.
  ```

**24. In how many ways can you pass parameters to a method in C#?**  
- By value (default): A copy of the variable is passed.  
- By reference (`ref`): The original variable can be modified.  
- Out parameters (`out`): Used for returning multiple values.  
- *Example*:  
  ```csharp  
  void UpdateValue(ref int value) { value = 10; }  
  int num = 5;  
  UpdateValue(ref num);  
  // Applied ref parameters to optimize reusable utilities.
  ```

**25. What are dynamic type variables in C#?**  
- The `dynamic` type allows variables to hold any type, determined at runtime.  
- It bypasses compile-time type checking.  
- Use with caution as it may cause runtime errors.  
- *Example*:  
  ```csharp  
  dynamic data = 5;  
  data = "Hello";  
  Console.WriteLine(data);  
  // Utilized dynamic types to handle JSON data with unknown structures.
  ```

**26. What is an enum in C#?**  
- An enum is a value type that defines a set of named constants.  
- It improves code readability and maintainability.  
- Enums are strongly typed and cannot be implicitly converted to other types.  
- *Example*:  
  ```csharp  
  enum Status { Active, Inactive, Suspended }  
  Status userStatus = Status.Active;  
  // Used enums to represent order statuses in an e-commerce platform.
  ```

**27. Is there a way to catch multiple exceptions at once without code duplication?**  
- Yes, use multiple `catch` blocks or a single block with a common base class like `Exception`.  
- Pattern matching can also differentiate exceptions in a single block.  
- Avoid excessive generalization to maintain clarity.  
- *Example*:  
  ```csharp  
  try { /* Code */ }  
  catch (FormatException) { /* Handle format issues */ }  
  catch (Exception ex) when (ex is IOException || ex is TimeoutException)  
  { Console.WriteLine("File or timeout error"); }  
  // Centralized error handling in an email client.
  ```

**28. Explain assignment vs shallow copy vs deep copy for a Record in C#?**  
- Assignment: Both variables point to the same object in memory.  
- Shallow copy: Copies the object but not its nested objects.  
- Deep copy: Copies the object and all nested objects.  
- *Example*:  
  ```csharp  
  var record1 = new MyRecord(1, "Data");  
  var record2 = record1 with { }; // Shallow copy using `with`.  
  // Applied these concepts to clone complex objects in a configuration manager.
  ```

**29. When to use Record, Class, or Struct in C#?**  
- Use `Record` for immutable data objects with value-based equality.  
- Use `Class` for reference types requiring flexibility and inheritance.  
- Use `Struct` for lightweight objects and small data representations.  
- *Example*:  
  ```csharp  
  record Customer(string Name, int Age);  
  struct Point { public int X, Y; }  
  // Designed customer data as Records for immutability in a retail system.
  ```

**30. Why can't you specify the accessibility modifier for methods inside the Interface in C#?**  
- All interface methods are implicitly public and abstract.  
- Accessibility modifiers are not allowed to enforce uniform access.  
- Interfaces define a contract, not implementation.  
- *Example*:  
  ```csharp  
  public interface IAnimal { void Speak(); }  
  // Ensured consistent access rules in service interface design for microservices.
  ```
  **31. What is Record in C#?**  
- A `Record` is a reference type designed for immutable data models with value-based equality.  
- Introduced in C# 9.0, it simplifies the creation of DTOs (Data Transfer Objects).  
- Supports "with" expressions to create modified copies of records.  
- *Example*:  
  ```csharp  
  public record Employee(string Name, int Age);  
  var emp1 = new Employee("John", 30);  
  var emp2 = emp1 with { Age = 31 };  
  // Used Records for designing immutability in financial reporting systems.
  ```

**32. What is an anonymous function in C#?**  
- An anonymous function is a function without a name, such as a lambda expression or a delegate.  
- Used for inline code logic and event handling.  
- Improves code readability in cases of short, reusable logic.  
- *Example*:  
  ```csharp  
  Func<int, int> square = x => x * x;  
  Console.WriteLine(square(5));  
  // Leveraged anonymous functions to implement quick calculations in a dashboard app.
  ```

**33. What is the use of the `IDisposable` interface?**  
- It defines a `Dispose` method for releasing unmanaged resources.  
- Commonly implemented in classes handling files, streams, or database connections.  
- Ensures deterministic cleanup of resources, often used with `using` statements.  
- *Example*:  
  ```csharp  
  public class FileManager : IDisposable  
  {  
      private FileStream _file;  
      public FileManager(string path) => _file = new FileStream(path, FileMode.Open);  
      public void Dispose() => _file?.Dispose();  
  }  
  // Implemented IDisposable in resource-heavy file processing services.
  ```

**34. Explain the difference between Task and Thread in .NET.**  
- A `Thread` represents a single execution path in a process.  
- A `Task` represents an asynchronous operation, often leveraging threads.  
- Tasks are higher-level abstractions and integrate well with the async/await model.  
- *Example*:  
  ```csharp  
  var task = Task.Run(() => Console.WriteLine("Running in Task"));  
  task.Wait();  
  // Used tasks to optimize background operations in a real-time analytics tool.
  ```

**35. What is a sealed class in C#?**  
- A sealed class cannot be inherited, ensuring its behavior remains unchanged.  
- It improves security and prevents misuse in extensible systems.  
- Marked with the `sealed` keyword before the class definition.  
- *Example*:  
  ```csharp  
  public sealed class Logger { public void Log(string message) => Console.WriteLine(message); }  
  // Used sealed classes for logging to prevent unintended modifications in production systems.
  ```

**36. What is the difference between overloading and overriding in C#?**  
- Overloading allows multiple methods in the same class with different parameter lists.  
- Overriding modifies a base class method in a derived class with the `override` keyword.  
- Overloading occurs at compile-time; overriding happens at runtime.  
- *Example*:  
  ```csharp  
  public class Base { public virtual void Display() => Console.WriteLine("Base"); }  
  public class Derived : Base { public override void Display() => Console.WriteLine("Derived"); }  
  // Overriding was used in a polymorphic system for dynamic dispatch.
  ```

**37. What is a lambda expression in C#?**  
- A lambda expression is a concise way to represent an anonymous method.  
- Syntax: `(parameters) => expression or statement block`.  
- Commonly used in LINQ queries and functional programming.  
- *Example*:  
  ```csharp  
  var square = (int x) => x * x;  
  Console.WriteLine(square(5));  
  // Applied lambda expressions to streamline query operations in a repository pattern.
  ```

**38. How is encapsulation implemented in C#?**  
- Encapsulation restricts direct access to class members by using access modifiers.  
- Members are exposed via properties and methods.  
- Improves code maintainability and security by hiding internal implementation.  
- *Example*:  
  ```csharp  
  public class Account  
  {  
      private decimal balance;  
      public decimal Balance { get => balance; private set => balance = value; }  
      public void Deposit(decimal amount) => Balance += amount;  
  }  
  // Encapsulation ensured secure updates to bank account data in a finance application.
  ```

**39. What is Reflection in C#?**  
- Reflection allows the inspection and manipulation of metadata at runtime.  
- It enables accessing information about assemblies, types, and members.  
- Commonly used for dynamic type discovery and late binding.  
- *Example*:  
  ```csharp  
  var type = typeof(String);  
  Console.WriteLine($"Methods of {type}: {string.Join(", ", type.GetMethods().Select(m => m.Name))}");  
  // Used reflection to dynamically load plugins in a modular application.
  ```

**40. How can you prevent a class from being overridden in C#?**  
- Mark the class with the `sealed` keyword.  
- Alternatively, mark specific methods as `sealed` in derived classes.  
- Prevents unintended modifications to critical functionality.  
- *Example*:  
  ```csharp  
  public sealed class FinalClass { public void Show() => Console.WriteLine("Cannot override me."); }  
  // Designed sealed classes for finalizing implementations in core utilities.
  ```

**41. What is the use of the Null Coalescing Operator (`??`) in C#?**  
- It provides a default value when a nullable type or expression is null.  
- Syntax: `value ?? defaultValue`.  
- Simplifies null checks and fallback value assignments.  
- *Example*:  
  ```csharp  
  string name = null;  
  Console.WriteLine(name ?? "Unknown");  
  // Employed null coalescing for safe fallback handling in customer data processing.
  ```

**42. What is a Destructor in C# and when should I create one?**  
- A destructor is used to release unmanaged resources when an object is garbage collected.  
- Syntax: `~ClassName()`.  
- Use only when handling unmanaged resources not covered by `IDisposable`.  
- *Example*:  
  ```csharp  
  public class FileHandler  
  {  
      ~FileHandler() { Console.WriteLine("Destructor called."); }  
  }  
  // Implemented destructors sparingly to finalize unmanaged resources in legacy components.
  ```

**43. What is the difference between Interface and Abstract Class in C#?**  
- Interfaces cannot contain implementation; abstract classes can have partial implementation.  
- A class can implement multiple interfaces but inherit only one abstract class.  
- Use interfaces for defining contracts and abstract classes for common behavior.  
- *Example*:  
  ```csharp  
  public interface IDrive { void Drive(); }  
  public abstract class Vehicle { public abstract void StartEngine(); }  
  // Designed abstract base classes and interfaces for flexible hierarchy in a transport system.
  ```

**44. What is the difference between constant and readonly in C#?**  
- `const` values are compile-time constants, while `readonly` values are runtime constants.  
- `const` must be assigned at declaration, `readonly` can be set in the constructor.  
- `const` is static by default; `readonly` applies to instance or static fields.  
- *Example*:  
  ```csharp  
  public const double Pi = 3.14;  
  public readonly DateTime CreatedOn = DateTime.Now;  
  // Used readonly fields to set initialization-time values in configuration classes.
  ```

**45. Explain the Anonymous type in C#.**  
- An anonymous type is a lightweight object without explicitly defining its type.  
- Syntax: `var obj = new { Property1 = Value1, Property2 = Value2 };`.  
- Commonly used in LINQ projections.  
- *Example*:  
  ```csharp  
  var person = new { Name = "John", Age = 30 };  
  Console.WriteLine($"Name: {person.Name}, Age: {person.Age}");  
  // Utilized anonymous types for ad-hoc query results in a reporting system.
  ```
  **46. Is there a difference between throw and throw ex in C#?**  
- `throw` preserves the original stack trace of the exception.  
- `throw ex` resets the stack trace, losing the original exception's context.  
- Always prefer `throw` unless there's a specific need to reset or log.  
- *Example*:  
  ```csharp  
  try  
  {  
      int x = 0;  
      int y = 10 / x;  
  }  
  catch (Exception ex)  
  {  
      Console.WriteLine("Logging exception");  
      throw; // Keeps the original stack trace.  
  }  
  ```

**47. Explain Code Compilation in C#.**  
- C# code compilation involves transforming source code into Intermediate Language (IL).  
- The compiler generates an assembly (.exe or .dll) containing IL.  
- At runtime, the Common Language Runtime (CLR) converts IL to machine code using Just-In-Time (JIT) compilation.  
- *Example*:  
  ```plaintext  
  Source Code → C# Compiler → IL (Intermediate Language) → JIT Compilation → Machine Code  
  ```

**48. What is the difference between Equality Operator (`==`) and `Equals()` method in C#?**  
- `==` compares object references for reference types and values for value types.  
- `Equals()` can be overridden for custom comparison logic.  
- Use `Equals()` for value-based equality in complex objects.  
- *Example*:  
  ```csharp  
  string s1 = "hello";  
  string s2 = "hello";  
  Console.WriteLine(s1 == s2); // True  
  Console.WriteLine(s1.Equals(s2)); // True  
  ```

**49. What are the uses of `using` in C#?**  
- Ensures deterministic cleanup of resources like file streams or database connections.  
- Automatically calls `Dispose()` at the end of the block.  
- Reduces the risk of resource leaks in managed code.  
- *Example*:  
  ```csharp  
  using (var reader = new StreamReader("file.txt"))  
  {  
      Console.WriteLine(reader.ReadToEnd());  
  }  
  ```

**50. What is the difference between dynamic type variables and object type variables in C#?**  
- `dynamic` variables bypass compile-time type checking; `object` requires casting.  
- `dynamic` variables allow operations determined at runtime.  
- Use `dynamic` cautiously as it reduces type safety.  
- *Example*:  
  ```csharp  
  dynamic dyn = "hello";  
  Console.WriteLine(dyn.Length); // No compile-time error  
  ```

**51. What is a Virtual Method in C#?**  
- A virtual method allows overriding in derived classes.  
- Declared with the `virtual` keyword in the base class.  
- Enhances polymorphism by enabling runtime method selection.  
- *Example*:  
  ```csharp  
  public class Base  
  {  
      public virtual void Display() => Console.WriteLine("Base");  
  }  
  public class Derived : Base  
  {  
      public override void Display() => Console.WriteLine("Derived");  
  }  
  ```

**52. What is the difference between Virtual and Abstract method in C#?**  
- A virtual method has a default implementation; an abstract method does not.  
- Abstract methods are declared in abstract classes.  
- Virtual methods can be optionally overridden; abstract methods must be.  
- *Example*:  
  ```csharp  
  public abstract class Animal  
  {  
      public abstract void Speak(); // No implementation  
  }  
  public class Dog : Animal  
  {  
      public override void Speak() => Console.WriteLine("Woof!");  
  }  
  ```

**53. What is the scope of an Internal member variable of a C# class?**  
- `internal` members are accessible within the same assembly.  
- They are not visible to other assemblies unless explicitly specified via `InternalsVisibleTo`.  
- Ideal for encapsulating details within a library.  
- *Example*:  
  ```csharp  
  internal class MyClass  
  {  
      internal void Display() => Console.WriteLine("Internal");  
  }  
  ```

**54. What is an Extension Method in C# and how to use them?**  
- Adds methods to existing types without modifying them.  
- Declared in static classes with the `this` keyword for the first parameter.  
- Widely used to enhance LINQ capabilities.  
- *Example*:  
  ```csharp  
  public static class StringExtensions  
  {  
      public static int WordCount(this string str) => str.Split(' ').Length;  
  }  
  Console.WriteLine("Hello World".WordCount());  
  ```

**55. What is the difference between `ref` and `out` keywords in C#?**  
- `ref` requires the variable to be initialized before passing.  
- `out` requires the variable to be assigned inside the method.  
- Both allow passing variables by reference, enabling modification.  
- *Example*:  
  ```csharp  
  void Calculate(out int x) { x = 10; }  
  Calculate(out int result);  
  Console.WriteLine(result); // Outputs 10  
  ```

**56. Can you create a function in C# which can accept varying numbers of arguments?**  
- Use the `params` keyword to accept a variable number of arguments.  
- All arguments must be of the same type.  
- Simplifies method calls for collections of data.  
- *Example*:  
  ```csharp  
  public void PrintParams(params int[] numbers)  
  {  
      foreach (var num in numbers)  
          Console.WriteLine(num);  
  }  
  PrintParams(1, 2, 3, 4);  
  ```

**57. What are pointer types in C#?**  
- Pointer types directly store the memory address of another variable.  
- Allowed only in `unsafe` context and require explicit enabling.  
- Used in performance-critical scenarios like interacting with hardware.  
- *Example*:  
  ```csharp  
  unsafe  
  {  
      int x = 10;  
      int* ptr = &x;  
      Console.WriteLine((int)ptr);  
  }  
  ```

**58. What is the difference between Dispose and Finalize methods in C#?**  
- `Dispose` is called explicitly for releasing resources; `Finalize` is invoked by the GC.  
- `Dispose` is part of the `IDisposable` interface.  
- Finalizers should be avoided unless dealing with unmanaged resources.  
- *Example*:  
  ```csharp  
  public void Dispose() => fileStream.Dispose();  
  ```

**59. What's the difference between `StackOverflowException` and `OutOfMemoryException` in C#?**  
- `StackOverflowException` occurs due to excessive recursion.  
- `OutOfMemoryException` happens when the heap runs out of memory.  
- Both are critical and usually unrecoverable.  
- *Example*:  
  ```plaintext  
  Recursive function without exit condition → StackOverflowException  
  Large memory allocations → OutOfMemoryException  
  ```

**60. What is an Indexer in C#?**  
- Indexers enable a class to be indexed like an array.  
- Defined using the `this` keyword with parameters.  
- Used to simplify accessing collections.  
- *Example*:  
  ```csharp  
  public class SampleCollection  
  {  
      private string[] data = new string[10];  
      public string this[int index] { get => data[index]; set => data[index] = value; }  
  }  
  ```  
  **61. What is the difference between `Func<string, string>` and `delegate` in C#?**  
- `Func<string, string>` is a predefined delegate for methods that take a string as input and return a string.  
- `delegate` is a user-defined type for referencing methods with custom signatures.  
- `Func` is concise and reusable for standard method signatures, while `delegate` offers flexibility.  
- *Example*:  
  ```csharp  
  Func<string, string> greet = name => $"Hello, {name}!";  
  Console.WriteLine(greet("John")); // Outputs: Hello, John!  

  delegate string CustomGreet(string name);  
  CustomGreet greetDelegate = name => $"Hi, {name}!";  
  Console.WriteLine(greetDelegate("John")); // Outputs: Hi, John!  
  ```

**62. Explain what is Short-Circuit Evaluation in C#.**  
- In `&&` (AND) and `||` (OR) operations, evaluation stops as soon as the result is determined.  
- Prevents unnecessary computation and potential runtime errors.  
- Applies only to logical operators, not bitwise operators like `&` or `|`.  
- *Example*:  
  ```csharp  
  int x = 5;  
  if (x > 0 && x / 0 == 1) // Division by zero is never evaluated due to short-circuiting.  
      Console.WriteLine("This won't run.");  
  ```

**63. Explain the difference between `Select` and `Where` in LINQ.**  
- `Select` is used to transform or project data into a new form.  
- `Where` is used to filter data based on a condition.  
- Both can be combined for filtering and transformation.  
- *Example*:  
  ```csharp  
  var numbers = new[] { 1, 2, 3, 4 };  
  var evenSquares = numbers.Where(n => n % 2 == 0).Select(n => n * n);  
  Console.WriteLine(string.Join(", ", evenSquares)); // Outputs: 4, 16  
  ```

**64. What is the best practice to achieve optimal performance using Lazy objects?**  
- Use `Lazy<T>` to defer initialization until the value is accessed.  
- Configure thread-safety with the appropriate constructor.  
- Avoid heavy computations in the Lazy factory method that negate its benefits.  
- *Example*:  
  ```csharp  
  Lazy<string> lazyValue = new Lazy<string>(() => ComputeValue());  
  string result = lazyValue.Value; // ComputeValue() is called only here.  
  ```

**65. What is a static constructor in C#?**  
- A static constructor initializes static data members of a class.  
- It is called automatically before the first instance is created or any static member is accessed.  
- There is no access modifier, and it cannot take parameters.  
- *Example*:  
  ```csharp  
  public class Example  
  {  
      static Example() => Console.WriteLine("Static constructor called.");  
      public static int Value = 10;  
  }  
  ```

**66. Explain what is Ternary Search.**  
- A divide-and-conquer algorithm similar to binary search but splits the array into three parts.  
- Used for unimodal functions or sorted arrays.  
- Less efficient than binary search due to additional comparisons.  
- *Example*:  
  ```plaintext  
  Given an array [1, 3, 5, 7], find the target by dividing the range into three sections.  
  ```

**67. Explain how asynchronous tasks with `async`/`await` work in .NET.**  
- `async` marks a method as asynchronous, allowing the use of `await`.  
- `await` pauses execution until the awaited task completes.  
- Improves responsiveness by freeing threads for other operations during wait times.  
- *Example*:  
  ```csharp  
  public async Task<string> GetDataAsync()  
  {  
      await Task.Delay(1000);  
      return "Data retrieved";  
  }  
  ```

**68. What happens when we Box or Unbox Nullable types in C#?**  
- Boxing converts a nullable type to `object`.  
- Unboxing assigns a boxed value back to a nullable type.  
- Null values remain null after boxing/unboxing.  
- *Example*:  
  ```csharp  
  int? num = 5;  
  object boxed = num;  
  int? unboxed = (int?)boxed;  
  ```

**69. Can you explain the difference between Interface, Abstract Class, Sealed Class, Static Class, and Partial Class in C#?**  
- **Interface**: Defines a contract; no implementation.  
- **Abstract Class**: Can have abstract methods and implemented methods.  
- **Sealed Class**: Cannot be inherited.  
- **Static Class**: Contains only static members.  
- **Partial Class**: Splits the definition into multiple files.  
- *Example*:  
  ```csharp  
  public abstract class Shape { public abstract void Draw(); } // Abstract  
  public interface IDrawable { void Draw(); } // Interface  
  public sealed class Circle : Shape { public override void Draw() => Console.WriteLine("Circle"); } // Sealed  
  public static class Utils { public static void Print() => Console.WriteLine("Static"); } // Static  
  ```

**70. How to solve Circular Reference problems in C#?**  
- Use weak references to prevent strong dependency cycles.  
- Leverage `IDisposable` and proper resource management.  
- Avoid circular dependencies in object graphs.  
- *Example*:  
  ```csharp  
  WeakReference obj = new WeakReference(new MyClass());  
  ```

**71. Test if a number belongs to the Fibonacci Series.**  
- A number `n` is Fibonacci if `5n² + 4` or `5n² - 4` is a perfect square.  
- Use a helper function to check if a number is a perfect square.  
- Efficient for checking membership without generating the series.  
- *Example*:  
  ```csharp  
  bool IsFibonacci(int n) => IsPerfectSquare(5 * n * n + 4) || IsPerfectSquare(5 * n * n - 4);  
  bool IsPerfectSquare(int x) => Math.Sqrt(x) % 1 == 0;  
  ```

**72. What is the output of the program below? Explain.**  
- Provide the code snippet to explain the behavior.  
- Discuss concepts like scope, static behavior, or threading as relevant.  
- Illustrate edge cases where applicable.  

**73. Can you do Iterative Pre-order Traversal of a Binary Tree without Recursion?**  
- Use a stack to simulate recursion for traversing the tree.  
- Push and pop nodes to visit in pre-order (root, left, right).  
- Avoid recursion to prevent stack overflow for large trees.  
- *Example*:  
  ```csharp  
  void PreOrder(Node root)  
  {  
      var stack = new Stack<Node>();  
      stack.Push(root);  
      while (stack.Count > 0)  
      {  
          Node current = stack.Pop();  
          Console.WriteLine(current.Value);  
          if (current.Right != null) stack.Push(current.Right);  
          if (current.Left != null) stack.Push(current.Left);  
      }  
  }  
  ```

**74. Can you return multiple values from a function in C#? Provide some examples.**  
- Use `out` parameters or return a tuple for multiple values.  
- Simplifies data handling when multiple results are needed.  
- *Example*:  
  ```csharp  
  (int, int) GetDimensions() => (5, 10);  
  var (width, height) = GetDimensions();  
  Console.WriteLine($"Width: {width}, Height: {height}");  
  ```

**75. Given an array of ints, write a C# method to total all the values that are even numbers.**  
- Use LINQ for concise filtering and summation.  
- Enhances readability and reduces boilerplate code.  
- *Example*:  
  ```csharp  
  int TotalEvenNumbers(int[] numbers) => numbers.Where(n => n % 2 == 0).Sum();  
  ```  
  **76. Refactor the code provided.**  
- Refactoring involves improving code readability, maintainability, and performance without changing its behavior.  
- Apply principles like DRY (Don't Repeat Yourself), SOLID, and design patterns.  
- Ensure to write test cases before and after refactoring to confirm correctness.  
- *Example*: Before:  
  ```csharp  
  if (x > 0) Console.WriteLine("Positive");  
  else if (x == 0) Console.WriteLine("Zero");  
  else Console.WriteLine("Negative");  
  ```  
  After:  
  ```csharp  
  Console.WriteLine(x > 0 ? "Positive" : x == 0 ? "Zero" : "Negative");  
  ```

**77. Explain how the Sentinel Search works.**  
- A linear search algorithm that places a sentinel (special marker) at the end of the array.  
- Reduces the number of boundary checks during iteration.  
- Useful for unsorted arrays with frequent searches.  
- *Example*:  
  ```csharp  
  int SentinelSearch(int[] arr, int key)  
  {  
      int last = arr[^1];  
      arr[^1] = key;  
      int i = 0;  
      while (arr[i] != key) i++;  
      arr[^1] = last;  
      return i < arr.Length - 1 || arr[^1] == key ? i : -1;  
  }  
  ```

**78. Reverse the ordering of words in a string.**  
- Split the string into words, reverse the array, and join them back.  
- Handles extra spaces appropriately.  
- *Example*:  
  ```csharp  
  string ReverseWords(string input)  
  {  
      return string.Join(" ", input.Split(' ', StringSplitOptions.RemoveEmptyEntries).Reverse());  
  }  
  Console.WriteLine(ReverseWords("Hello World!")); // Outputs: World! Hello  
  ```

**79. How to check if two strings (words) are anagrams?**  
- Two strings are anagrams if their sorted characters match.  
- Ignore case and spaces for accurate comparison.  
- *Example*:  
  ```csharp  
  bool AreAnagrams(string str1, string str2)  
  {  
      return string.Concat(str1.ToLower().OrderBy(c => c)) == string.Concat(str2.ToLower().OrderBy(c => c));  
  }  
  Console.WriteLine(AreAnagrams("listen", "silent")); // Outputs: True  
  ```

**80. What is the output of the short program below? Explain.**  
- Present the program and describe the logic step-by-step.  
- Discuss specific constructs like loops, recursion, or LINQ as applicable.  
- Provide a practical example showing edge cases.  

**81. What is the Fibonacci Search technique?**  
- A searching algorithm that uses Fibonacci numbers to split the array.  
- Reduces the search range based on Fibonacci proportions.  
- Suitable for sorted and uniformly distributed data.  
- *Example*:  
  ```plaintext  
  Use Fibonacci numbers to narrow down search intervals in an array.  
  ```

**82. Is relying on `&&` short-circuiting safe in .NET?**  
- Yes, it prevents evaluation of subsequent conditions if the first condition fails.  
- Avoids potential runtime errors like null reference exceptions.  
- Only use short-circuiting where conditions are guaranteed to follow an order.  
- *Example*:  
  ```csharp  
  if (obj != null && obj.Property == value) // Safe from null reference errors.  
      Console.WriteLine("Valid.");  
  ```

**83. Find the Merge (Intersection) Point of Two Linked Lists.**  
- Use two pointers, each traversing one list.  
- When a pointer reaches the end, move it to the start of the other list.  
- The intersection point is where the pointers meet.  
- *Example*:  
  ```csharp  
  Node FindIntersection(Node headA, Node headB)  
  {  
      Node p1 = headA, p2 = headB;  
      while (p1 != p2)  
      {  
          p1 = p1 == null ? headB : p1.Next;  
          p2 = p2 == null ? headA : p2.Next;  
      }  
      return p1;  
  }  
  ```

**84. Binet's formula: How to calculate Fibonacci numbers without recursion or iteration?**  
- Binet's formula uses the golden ratio to calculate Fibonacci numbers.  
- Provides an exact result for small numbers but suffers rounding errors for large indices.  
- *Example*:  
  ```csharp  
  double Fibonacci(int n)  
  {  
      double phi = (1 + Math.Sqrt(5)) / 2;  
      return Math.Round(Math.Pow(phi, n) / Math.Sqrt(5));  
  }  
  ```

**85. What is the output of the program below? Explain your answer.**  
- Analyze the program and explain its logic clearly.  
- Discuss potential pitfalls like variable scope or initialization.  
- Use comments to clarify each step of the explanation.  

**86. Is the comparison of `time` and `null` in an `if` statement valid or not? Why or why not?**  
- Valid if `time` is a nullable type or reference type.  
- Invalid for value types like `DateTime` unless it’s nullable.  
- *Example*:  
  ```csharp  
  DateTime? time = null;  
  if (time == null) Console.WriteLine("Time is null.");  
  ```

**87. Calculate the circumference of a circle.**  
- Use the formula `C = 2 * π * r`, where `r` is the radius.  
- Leverage constants like `Math.PI` for accuracy.  
- *Example*:  
  ```csharp  
  double Circumference(double radius) => 2 * Math.PI * radius;  
  Console.WriteLine(Circumference(5)); // Outputs: 31.4159...  
  ```

**88. What is the difference between `as` and `is` keywords in C#?**  
- `is` checks if an object is of a specified type and returns a boolean.  
- `as` casts an object to the specified type or returns `null` if the cast fails.  
- Use `is` for type checking and `as` for safe casting.  
- *Example*:  
  ```csharp  
  object obj = "Hello";  
  if (obj is string str) Console.WriteLine(str); // Safe type pattern matching.  
  string result = obj as string; // Safe casting.  
  ```

**89. How can you implement multi-threading in C#?**  
- Use `Thread`, `Task`, or `Parallel` classes for concurrent execution.  
- Ensure proper synchronization to avoid race conditions.  
- Use `async`/`await` for asynchronous programming.  
- *Example*:  
  ```csharp  
  Task.Run(() => Console.WriteLine("Running in a separate thread."));  
  ```

**90. What is the role of a thread pool in C#?**  
- Manages a pool of worker threads for efficient task execution.  
- Reduces overhead by reusing threads instead of creating new ones.  
- Optimized for short-lived and repetitive tasks.  
- *Example*:  
  ```csharp  
  ThreadPool.QueueUserWorkItem(_ => Console.WriteLine("Thread pool example."));  
  ```

  **91. How do you handle memory leaks in C#?**  
- Avoid unmanaged resources or release them promptly using the `Dispose` method.  
- Use the `using` statement to ensure proper disposal of resources.  
- Regularly profile and monitor memory usage with tools like dotMemory.  
- *Example*:  
  ```csharp  
  using (var resource = new StreamReader("file.txt"))  
  {  
      Console.WriteLine(resource.ReadToEnd());  
  } // Automatically disposes the StreamReader.  
  ```

**92. What is the role of garbage collection in C#?**  
- Automatically manages memory allocation and deallocation.  
- Identifies and frees unused objects to prevent memory leaks.  
- Operates in generations (0, 1, 2) for efficiency.  
- *Example*:  
  ```csharp  
  GC.Collect(); // Explicitly triggers garbage collection (rarely needed).  
  ```

**93. Can you explain the significance of the `async` keyword in C#?**  
- Marks methods as asynchronous to enable non-blocking execution.  
- Used with `await` to handle asynchronous tasks.  
- Improves application responsiveness, especially in I/O-bound operations.  
- *Example*:  
  ```csharp  
  async Task<string> FetchDataAsync()  
  {  
      await Task.Delay(1000);  
      return "Data fetched";  
  }  
  ```

**94. What is the difference between `ref` and `out` parameters in C#?**  
- `ref` requires the variable to be initialized before passing.  
- `out` allows the variable to be uninitialized but must be assigned in the method.  
- Both pass arguments by reference, allowing modifications.  
- *Example*:  
  ```csharp  
  void SetValues(ref int a, out int b)  
  {  
      a *= 2;  
      b = 10;  
  }  
  int x = 5, y;  
  SetValues(ref x, out y);  
  ```

**95. What are the advantages of using `var` in C#?**  
- Simplifies code by inferring the type at compile time.  
- Reduces redundancy in declarations, improving readability.  
- Useful for LINQ queries or anonymous types.  
- *Example*:  
  ```csharp  
  var numbers = new List<int> { 1, 2, 3 };  
  ```

**96. How does the `yield` keyword work in C#?**  
- Produces a sequence of values in an iterator without creating an entire collection.  
- Suspends execution and resumes from the last `yield` statement.  
- Efficient for large or infinite data streams.  
- *Example*:  
  ```csharp  
  IEnumerable<int> GenerateNumbers()  
  {  
      for (int i = 0; i < 5; i++)  
          yield return i;  
  }  
  ```

**97. What is the difference between a `delegate` and an `event` in C#?**  
- A `delegate` is a type that holds a reference to methods.  
- An `event` is a wrapper over a delegate that restricts direct invocation.  
- `event` provides better encapsulation and is used for publish/subscribe patterns.  
- *Example*:  
  ```csharp  
  public delegate void Notify();  
  public event Notify OnNotify;  
  ```

**98. How do you implement the Singleton pattern in C#?**  
- Ensures a class has only one instance and provides a global access point.  
- Use a private constructor and a static instance.  
- Thread-safe implementation involves locking or `Lazy<T>`.  
- *Example*:  
  ```csharp  
  public sealed class Singleton  
  {  
      private static readonly Lazy<Singleton> instance = new(() => new Singleton());  
      private Singleton() { }  
      public static Singleton Instance => instance.Value;  
  }  
  ```

**99. What is a static class in C# and when should it be used?**  
- A static class cannot be instantiated and only contains static members.  
- Ideal for utility functions, constants, or extension methods.  
- Enhances performance by eliminating the need for object creation.  
- *Example*:  
  ```csharp  
  public static class MathUtils  
  {  
      public static int Add(int a, int b) => a + b;  
  }  
  ```

**100. What is the role of an Interface in C#?**  
- Defines a contract that implementing classes must follow.  
- Supports multiple inheritance by implementing multiple interfaces.  
- Facilitates loose coupling and testability.  
- *Example*:  
  ```csharp  
  public interface IVehicle  
  {  
      void Start();  
  }  
  public class Car : IVehicle  
  {  
      public void Start() => Console.WriteLine("Car started.");  
  }  
  ```

**101. How do you define a constant in C#?**  
- Use the `const` keyword for compile-time constants.  
- Use `readonly` for runtime constants.  
- Constants improve code readability and prevent accidental modification.  
- *Example*:  
  ```csharp  
  const double Pi = 3.14159;  
  ```

**102. How do you use a lambda expression with LINQ in C#?**  
- Lambda expressions define inline functions for LINQ operations.  
- Commonly used with methods like `Where`, `Select`, and `OrderBy`.  
- Simplifies filtering and transforming data collections.  
- *Example*:  
  ```csharp  
  var evenNumbers = numbers.Where(n => n % 2 == 0);  
  ```

**103. What is a "null" reference exception in C#?**  
- Occurs when attempting to access members of a null object.  
- Prevented using null checks or the null conditional operator (`?.`).  
- Avoided with nullable reference types (`?`) and `null` coalescing.  
- *Example*:  
  ```csharp  
  string? name = null;  
  Console.WriteLine(name?.Length);  
  ```

**104. How can you prevent a class from being instantiated in C#?**  
- Mark the class as `static` or use a private constructor.  
- Prevents unintended usage while exposing functionality.  
- Common for utility or helper classes.  
- *Example*:  
  ```csharp  
  public static class Utilities  
  {  
      public static void DoWork() => Console.WriteLine("Working!");  
  }  
  ```

**105. What is a thread-safe collection in C#?**  
- A collection designed to handle concurrent access without data corruption.  
- Examples include `ConcurrentDictionary` and `BlockingCollection`.  
- Ideal for multi-threaded applications.  
- *Example*:  
  ```csharp  
  var dict = new ConcurrentDictionary<int, string>();  
  dict.TryAdd(1, "Value1");  
  ```

There are **25 questions remaining** (106 to 130). Here's the completion:

---

**106. What is the difference between `try-catch` and `try-finally` in C#?**  
- `try-catch` is used for handling exceptions, where the `catch` block processes errors.  
- `try-finally` ensures cleanup or final steps regardless of exceptions.  
- Use `try-catch` for error handling and `try-finally` for cleanup.  
- *Example*:  
  ```csharp  
  try  
  {  
      int result = 10 / 0;  
  }  
  finally  
  {  
      Console.WriteLine("Cleanup executed.");  
  }  
  ```

**107. How do you implement dependency injection in C#?**  
- Inject dependencies into a class via constructor, property, or method.  
- Promotes loose coupling and testability.  
- Use frameworks like ASP.NET Core's built-in DI container.  
- *Example*:  
  ```csharp  
  public class Service { }  
  public class Consumer  
  {  
      private readonly Service _service;  
      public Consumer(Service service) => _service = service;  
  }  
  ```

**108. What is a collection initializer in C#?**  
- Allows initializing collections with values at the time of declaration.  
- Reduces boilerplate code.  
- Works with any collection that implements `ICollection<T>`.  
- *Example*:  
  ```csharp  
  var numbers = new List<int> { 1, 2, 3, 4 };  
  ```

**109. How do you implement deep cloning in C#?**  
- Use serialization or manual member-wise copy for deep cloning.  
- Ensures all nested objects are cloned.  
- Use libraries like Newtonsoft.Json for simpler implementation.  
- *Example*:  
  ```csharp  
  var deepCopy = JsonConvert.DeserializeObject<MyClass>(JsonConvert.SerializeObject(original));  
  ```

**110. What are the different types of collections in C#?**  
- Non-generic: `ArrayList`, `Hashtable`, etc.  
- Generic: `List<T>`, `Dictionary<TKey, TValue>`, etc.  
- Concurrent: `ConcurrentBag<T>`, `ConcurrentDictionary<TKey, TValue>`.  
- *Example*:  
  ```csharp  
  var dict = new Dictionary<int, string> { { 1, "One" } };  
  ```

**111. What is the purpose of a constructor in C#?**  
- Initializes objects of a class.  
- Can be parameterized or parameterless.  
- Automatically invoked when an object is created.  
- *Example*:  
  ```csharp  
  public class Car  
  {  
      public Car(string model) { Model = model; }  
      public string Model { get; }  
  }  
  ```

**112. How do you make a class thread-safe in C#?**  
- Use locks, `Monitor`, or thread-safe collections.  
- Minimize shared resources and critical sections.  
- Use immutability for objects when possible.  
- *Example*:  
  ```csharp  
  private static readonly object lockObj = new();  
  lock (lockObj) { /* Critical section */ }  
  ```

**113. What is an iterator in C#?**  
- Used to traverse a collection using `yield` statements.  
- Implements `IEnumerable` or `IEnumerator`.  
- Simplifies creating custom collections.  
- *Example*:  
  ```csharp  
  public IEnumerable<int> GetNumbers()  
  {  
      for (int i = 0; i < 5; i++) yield return i;  
  }  
  ```

**114. How does a `using` statement work in C#?**  
- Ensures resources are disposed of automatically.  
- Commonly used with objects implementing `IDisposable`.  
- Shortens and simplifies resource management.  
- *Example*:  
  ```csharp  
  using (var resource = new StreamReader("file.txt"))  
  {  
      Console.WriteLine(resource.ReadToEnd());  
  }  
  ```

**115. What is the purpose of the `params` keyword in C#?**  
- Allows methods to accept a variable number of arguments.  
- Useful for simplifying parameter passing.  
- Accepts zero or more arguments as an array.  
- *Example*:  
  ```csharp  
  void Print(params int[] numbers)  
  {  
      foreach (var num in numbers) Console.WriteLine(num);  
  }  
  ```

**116. How does C# handle exception filtering?**  
- Enables conditional filtering using the `when` keyword.  
- Improves readability and separates exception handling logic.  
- Reduces nested `if` conditions in catch blocks.  
- *Example*:  
  ```csharp  
  catch (Exception ex) when (ex.Message.Contains("Specific Error"))  
  {  
      Console.WriteLine("Filtered exception.");  
  }  
  ```

**117. How do you handle exceptions in asynchronous methods in C#?**  
- Use `await` to capture exceptions in `try-catch`.  
- Handle exceptions in the `Task` returned by async methods.  
- Optionally use `Task.Exception` for unobserved exceptions.  
- *Example*:  
  ```csharp  
  try  
  {  
      await SomeAsyncMethod();  
  }  
  catch (Exception ex)  
  {  
      Console.WriteLine(ex.Message);  
  }  
  ```

**118. What are anonymous methods in C#?**  
- Methods without a name, defined inline using the `delegate` keyword.  
- Useful for short, simple operations.  
- Replaced by lambda expressions in most cases.  
- *Example*:  
  ```csharp  
  Action<int> print = delegate (int x) { Console.WriteLine(x); };  
  print(10);  
  ```

**119. What is the difference between `IEnumerable` and `IEnumerator` in C#?**  
- `IEnumerable` provides an iterator for a collection.  
- `IEnumerator` allows iteration with `MoveNext()` and `Current`.  
- `IEnumerable` is used for collection exposure; `IEnumerator` for iteration logic.  
- *Example*:  
  ```csharp  
  foreach (var item in collection) { /* Uses IEnumerable */ }  
  ```

**120. What are the differences between a class and a struct in C#?**  
- Classes are reference types, while structs are value types.  
- Classes support inheritance; structs do not.  
- Structs are lightweight and ideal for small data types.  
- *Example*:  
  ```csharp  
  struct Point { public int X, Y; }  
  ```

**121. How do you implement error handling in asynchronous methods in C#?**  
- Wrap `await` calls in `try-catch`.  
- Use `Task.ContinueWith` for additional handling.  
- Ensure tasks are awaited to capture exceptions.  
- *Example*:  
  ```csharp  
  try  
  {  
      await ProcessAsync();  
  }  
  catch (Exception ex)  
  {  
      Console.WriteLine(ex.Message);  
  }  
  ```

**122. What is the difference between `Array` and `List` in C#?**  
- `Array` is fixed-size, while `List` is dynamic.  
- `Array` provides better performance for fixed-size collections.  
- `List` supports many helper methods like `Add` and `Remove`.  
- *Example*:  
  ```csharp  
  List<int> numbers = new() { 1, 2, 3 };  
  ```

**123. What is the difference between a shallow copy and a deep copy of an object in C#?**  
- A shallow copy duplicates only the top-level structure.  
- A deep copy duplicates all referenced objects recursively.  
- Use serialization or cloning libraries for deep copies.  
- *Example*:  
  ```csharp  
  var deepCopy = JsonConvert.DeserializeObject<MyClass>(JsonConvert.SerializeObject(original));  
  ```

**124. What is the purpose of the `params` keyword in a method signature?**  
- Simplifies passing a variable number of parameters to a method.  
- Eliminates the need for creating arrays explicitly.  
- *Example*:  
  ```csharp  
  void Print(params string[] names) { foreach (var name in names) Console.WriteLine(name); }  
  ```

**125. What is the difference between `string` and `String` in C#?**  
- Both refer to `System.String`; `string` is an alias in C#.  
- `String` is used for accessing methods and properties explicitly.  
- Functionally identical but stylistically different.  
- *Example*:  
  ```csharp  
  string name = "John";  
  String upperName = name.ToUpper();  
  ```

**126. How do you use a constructor with parameters in C#?**  
- Define parameters in the constructor to initialize fields.  
- Invoke using the `new` keyword with arguments.  
- *Example*:  
  ```csharp  
  public Person(string name, int age) { Name = name; Age = age; }  
  ```

**127. What is the importance of `finally` in exception handling in C#?**  
- Ensures code runs regardless of exceptions.  
- Ideal for releasing resources or cleanup.  
- *Example*:  
  ```csharp  
  try { /* Work */ } finally

 { Console.WriteLine("Cleanup"); }  
  ```

**128. How do you create a read-only property in C#?**  
- Define a property with only a `get` accessor.  
- Use `readonly` keyword for backing fields.  
- *Example*:  
  ```csharp  
  public int Age { get; } = 30;  
  ```

**129. What is the difference between a static method and an instance method in C#?**  
- Static methods belong to the class; instance methods to objects.  
- Static methods do not require object instantiation.  
- *Example*:  
  ```csharp  
  public static int Add(int x, int y) => x + y;  
  ```

**130. How do you implement a generic method in C#?**  
- Define type parameters in the method signature.  
- Enables type-safe code reuse.  
- *Example*:  
  ```csharp  
  public T GetMax<T>(T a, T b) where T : IComparable<T>  
  {  
      return a.CompareTo(b) > 0 ? a : b;  
  }  
  ```  

---  