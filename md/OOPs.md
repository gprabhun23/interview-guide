### 1. What are the four principles of OOP?  
- **Encapsulation**: Bundles data and methods operating on that data into a single unit (class) and restricts direct access.  
- **Abstraction**: Hides implementation details and only exposes functionality.  
- **Inheritance**: Allows a class to acquire properties and behaviors of another class.  
- **Polymorphism**: Enables a single interface to represent different underlying forms (e.g., method overriding).  
- Example: In a project, I used inheritance to create specific vehicle classes from a general "Vehicle" base class, allowing reusability and extensibility.

### 2. How does encapsulation work in C#? How is encapsulation achieved in C#?  
- Encapsulation is achieved using access modifiers like `private`, `protected`, `internal`, and `public`.  
- It restricts access to class fields and methods, exposing only what's necessary.  
- Provides `get` and `set` accessors for controlled access to properties.  
- Helps maintain code modularity and protect the integrity of data.  
- Example:  
```csharp
class Employee {
    private string name;
    public string Name {
        get { return name; }
        set { name = value; }
    }
}
```  
This ensures `name` is only accessed through the property `Name`.

### 3. Explain the concept of inheritance with examples in C#. How does inheritance work in C#?  
- Inheritance allows a derived class to reuse and extend the functionality of a base class.  
- Achieved using the `:` syntax (e.g., `class Derived : Base`).  
- Promotes code reuse and logical hierarchy.  
- Supports method overriding for customizing behavior in derived classes.  
- Example:  
```csharp
class Vehicle {
    public void Start() => Console.WriteLine("Vehicle started");
}
class Car : Vehicle {
    public void Drive() => Console.WriteLine("Car is driving");
}
// Usage:
Car car = new Car();
car.Start();  // Inherited
car.Drive();  // Custom
```

### 4. What are abstract classes and interfaces, and how are they different? What are the advantages of using interfaces over abstract classes in C#?  
- Abstract classes can have methods with or without implementations, whereas interfaces only declare methods.  
- A class can inherit multiple interfaces but only one abstract class.  
- Abstract classes provide shared functionality; interfaces define contracts.  
- Interfaces promote loose coupling and flexibility in design.  
- Example: I used an interface `IDatabase` in a project to switch between SQL and NoSQL databases dynamically.  
```csharp
interface IDatabase {
    void Connect();
}
class SqlDatabase : IDatabase {
    public void Connect() => Console.WriteLine("Connected to SQL");
}
```

### 5. What is the use of virtual methods in C#?  
- Virtual methods allow derived classes to override a method defined in a base class.  
- Declared with the `virtual` keyword and overridden using `override`.  
- Enables polymorphism by allowing behavior to change in derived classes.  
- Supports dynamic dispatch of methods at runtime.  
- Example:  
```csharp
class Animal {
    public virtual void Speak() => Console.WriteLine("Animal speaks");
}
class Dog : Animal {
    public override void Speak() => Console.WriteLine("Dog barks");
}
// Usage:
Animal animal = new Dog();
animal.Speak();  // Output: Dog barks
```

### 6. Explain the concept of sealed classes in C#.  
- Sealed classes cannot be inherited.  
- Declared with the `sealed` keyword.  
- Useful for preventing further extension of critical functionality.  
- Enhances security and avoids unintended modifications.  
- Example:  
```csharp
sealed class FinalClass {
    public void Display() => Console.WriteLine("This is a sealed class");
}
```

### 7. What is an indexer in C#? Provide an example.  
- Indexers allow objects to be indexed like arrays.  
- Defined using the `this` keyword.  
- Simplify object data access without explicit method calls.  
- Useful for collections or data structures.  
- Example:  
```csharp
class BookCollection {
    private string[] books = new string[3];
    public string this[int index] {
        get => books[index];
        set => books[index] = value;
    }
}
// Usage:
BookCollection collection = new BookCollection();
collection[0] = "C# Basics";
Console.WriteLine(collection[0]);  // Output: C# Basics
```

### 8. How is multiple inheritance achieved in C#?  
- Multiple inheritance is not supported with classes but is achieved using interfaces.  
- A class can implement multiple interfaces.  
- Promotes better design by combining behaviors without complexity.  
- Avoids the "diamond problem" seen in other languages.  
- Example:  
```csharp
interface IReadable {
    void Read();
}
interface IWritable {
    void Write();
}
class Document : IReadable, IWritable {
    public void Read() => Console.WriteLine("Reading document");
    public void Write() => Console.WriteLine("Writing document");
}
```

### 9. What are constructors, and how do you implement different types of constructors in C#?  
- Constructors initialize an object when it is created.  
- Types: Default, Parameterized, Copy, and Static constructors.  
- Default constructors take no arguments; parameterized constructors take arguments.  
- Static constructors initialize static members.  
- Example:  
```csharp
class Person {
    public string Name { get; }
    public Person(string name) {
        Name = name;
    }
}
// Usage:
Person person = new Person("John");
```

### 10. What is the purpose of destructors in C#?  
- Destructors release resources before an object is reclaimed by the garbage collector.  
- Automatically invoked when the object goes out of scope.  
- Defined using a tilde (`~`) before the class name.  
- Used in unmanaged resource cleanup.  
- Example:  
```csharp
class Resource {
    ~Resource() {
        Console.WriteLine("Destructor called");
    }
}
```

### 11. Explain the significance of access modifiers in OOP.  
- Control the visibility and accessibility of class members.  
- Types: `public`, `private`, `protected`, `internal`, and `protected internal`.  
- Ensure encapsulation and prevent unauthorized access.  
- Facilitate the principle of least privilege.  
- Example:  
```csharp
class Example {
    private int data;
    public int Data {
        get => data;
        set => data = value;
    }
}
```

### 12. What is the purpose of the this keyword in C#?  
- Refers to the current instance of a class.  
- Differentiates between class members and parameters with the same name.  
- Passes the current object as a parameter.  
- Calls another constructor in the same class.  
- Example:  
```csharp
class Example {
    private int value;
    public Example(int value) {
        this.value = value;
    }
}
```

### 13. How does the Singleton pattern relate to OOP concepts?  
- Ensures a class has only one instance and provides a global access point.  
- Implements encapsulation, abstraction, and controlled instantiation.  
- Used for managing shared resources.  
- Example:  
```csharp
class Singleton {
    private static Singleton instance;
    private Singleton() {}
    public static Singleton Instance => instance ??= new Singleton();
}
```

### 14. What is polymorphism, and how is it implemented in C#? How do polymorphism and method overriding work in C#?  
- Polymorphism allows one interface to represent multiple types.  
- Achieved through method overriding (`virtual` and `override`) and interfaces.  
- Method overriding enables behavior modification in derived classes.  
- Supports runtime polymorphism.  
- Example:  
```csharp
class Shape {
    public virtual void Draw() => Console.WriteLine("Drawing shape");
}
class Circle : Shape {
    public override void Draw() => Console.WriteLine("Drawing circle");
}
```

### 15. What is the difference between an interface and an abstract class in OOP?  
- Abstract classes can have implementation; interfaces cannot.  
- Classes can inherit multiple interfaces but only one abstract class.  
- Interfaces define behavior contracts; abstract classes share common code.  
- Abstract classes support fields; interfaces do not.  
- Example: Abstract class used for base behavior, interface for external API communication.

Here are the next 15 questions. After this set, **15 questions** will remain pending from your original list.  

### 16. How does the virtual keyword work in C#, and why is it used?  
- Declares a method or property as overrideable in derived classes.  
- Allows derived classes to change behavior by using the `override` keyword.  
- Facilitates runtime polymorphism.  
- Ensures base class methods can provide default functionality while being extensible.  
- Example:  
```csharp
class Base {
    public virtual void Show() => Console.WriteLine("Base class");
}
class Derived : Base {
    public override void Show() => Console.WriteLine("Derived class");
}
```

### 17. How do you implement the Singleton design pattern in C#?  
- Ensure only one instance of the class exists using private constructors.  
- Use a static property or method to provide access to the instance.  
- Use thread-safe mechanisms for multi-threaded environments.  
- Lazy initialization is common to optimize resource usage.  
- Example:  
```csharp
class Singleton {
    private static Singleton instance;
    private Singleton() {}
    public static Singleton Instance => instance ??= new Singleton();
}
```

### 18. What is the difference between method overloading and method overriding?  
- **Method overloading**: Same method name, different parameter lists in the same class.  
- **Method overriding**: Redefining a base class method in a derived class using `virtual` and `override`.  
- Overloading is compile-time polymorphism; overriding is runtime polymorphism.  
- Overloading uses static resolution, while overriding uses dynamic resolution.  
- Example:  
```csharp
// Overloading
class Example {
    public void Show() {}
    public void Show(int num) {}
}
// Overriding
class Base {
    public virtual void Show() {}
}
class Derived : Base {
    public override void Show() {}
}
```

### 19. What are constructors, and how are they different from methods in OOP?  
- Constructors initialize objects and have the same name as the class.  
- Constructors are invoked automatically during object creation.  
- Cannot return a value, unlike methods.  
- Can be overloaded but not overridden.  
- Example:  
```csharp
class Example {
    public Example() => Console.WriteLine("Constructor called");
    public void Show() => Console.WriteLine("Method called");
}
```

### 20. How do you implement the Factory pattern in OOP?  
- Creates objects without specifying the exact class type.  
- Promotes loose coupling by using a common interface or base class.  
- Useful for creating objects with complex construction logic.  
- Example:  
```csharp
interface IShape {
    void Draw();
}
class Circle : IShape {
    public void Draw() => Console.WriteLine("Drawing circle");
}
class ShapeFactory {
    public static IShape GetShape(string type) {
        return type == "Circle" ? new Circle() : null;
    }
}
```

### 21. What is the purpose of a static class in C#?  
- Used to group utility or helper methods.  
- Cannot be instantiated or inherited.  
- All members must be static.  
- Provides a global point of access for shared methods or properties.  
- Example:  
```csharp
static class MathHelper {
    public static int Add(int a, int b) => a + b;
}
```

### 22. What are the principles of SOLID, and how do they relate to OOP?  
- **Single Responsibility Principle (SRP)**: A class should have one reason to change.  
- **Open/Closed Principle (OCP)**: Classes should be open for extension but closed for modification.  
- **Liskov Substitution Principle (LSP)**: Derived classes must be substitutable for their base classes.  
- **Interface Segregation Principle (ISP)**: Prefer smaller, specific interfaces over larger, general ones.  
- **Dependency Inversion Principle (DIP)**: Depend on abstractions, not concrete implementations.  
- Example: Using DI containers in a project ensures DIP by injecting dependencies.

### 23. Explain the concept of method hiding using the new keyword in C#.  
- Hides a base class method in the derived class without overriding it.  
- Declared using the `new` keyword in the derived class.  
- Useful for redefining base class members without affecting the base class behavior.  
- Does not support runtime polymorphism.  
- Example:  
```csharp
class Base {
    public void Display() => Console.WriteLine("Base display");
}
class Derived : Base {
    public new void Display() => Console.WriteLine("Derived display");
}
```

### 24. How does runtime polymorphism differ from compile-time polymorphism in OOP?  
- **Runtime polymorphism**: Achieved through method overriding using `virtual` and `override`.  
- **Compile-time polymorphism**: Achieved through method overloading or operator overloading.  
- Runtime polymorphism is resolved during execution; compile-time polymorphism is resolved at compile time.  
- Example:  
```csharp
// Runtime
class Base {
    public virtual void Show() => Console.WriteLine("Base");
}
class Derived : Base {
    public override void Show() => Console.WriteLine("Derived");
}
Base obj = new Derived();
obj.Show();  // Output: Derived
```

### 25. What is the role of a constructor in object initialization, and what are its types?  
- Initializes an object's state during its creation.  
- Types: Default, parameterized, copy, and static constructors.  
- Ensures objects are in a valid state before use.  
- Can include logic for dependency injection or resource initialization.  
- Example:  
```csharp
class Example {
    public Example() => Console.WriteLine("Default constructor");
    public Example(int id) => Console.WriteLine($"Parameterized: {id}");
}
```

### 26. How does the SOLID principle enhance object-oriented design, and what are practical examples of each principle?  
- Enhances code maintainability and scalability.  
- SRP: Separate classes for logging and data storage.  
- OCP: Plugin-based architecture.  
- LSP: Replaceable subclasses in collection classes.  
- ISP: Specific interfaces like `IReadable` and `IWritable`.  
- DIP: Constructor injection for database services.  

### 27. What is the difference between polymorphism at compile-time and runtime? Provide examples in C#.  
- Compile-time polymorphism uses overloading; runtime uses overriding.  
- Compile-time resolves at compile time; runtime resolves during execution.  
- Compile-time doesn't involve inheritance; runtime requires it.  
- Example:  
```csharp
// Compile-time
class MathOperations {
    public int Add(int a, int b) => a + b;
    public double Add(double a, double b) => a + b;
}
// Runtime
class Base {
    public virtual void Show() => Console.WriteLine("Base");
}
class Derived : Base {
    public override void Show() => Console.WriteLine("Derived");
}
```

### 28. How can you implement method overloading and overriding in an OOP language like C#?  
- **Method overloading**: Same method name, different parameters.  
- **Method overriding**: Derived class changes base class method using `virtual` and `override`.  
- Example:  
```csharp
class Base {
    public virtual void Show() => Console.WriteLine("Base");
}
class Derived : Base {
    public override void Show() => Console.WriteLine("Derived");
}
```

### 29. What are sealed classes in OOP, and when would you use them?  
- Classes marked `sealed` cannot be inherited.  
- Used to prevent further extension or overriding.  
- Useful for security and performance optimization.  
- Example:  
```csharp
sealed class Final {
    public void Show() => Console.WriteLine("Final class");
}
```

### 30. Explain the concept of association, aggregation, and composition with examples.  
- **Association**: A general relationship between two classes.  
- **Aggregation**: "Has-a" relationship where one class contains another but doesn't control its lifecycle.  
- **Composition**: Stronger "Has-a" relationship where the container class owns the lifecycle.  
- Example:  
```csharp
// Aggregation
class Engine {}
class Car {
    public Engine Engine { get; set; }
}
// Composition
class Computer {
    private Processor processor = new Processor();
}
```  

Here are the last 15 questions. This completes all the questions from your original list.  

### 31. What is the Liskov Substitution Principle, and how does it affect subclassing?  
- Derived classes must be replaceable for their base classes without affecting functionality.  
- Ensures objects of a superclass can be used wherever the base type is expected.  
- Violations occur when derived classes modify expected behavior or constraints.  
- Promotes reusable and interchangeable code.  
- Example: Using a `Rectangle` and `Square` where both adhere to a common `Shape` base class.  

```csharp
class Shape {
    public virtual int Area() => 0;
}
class Rectangle : Shape {
    public int Width { get; set; }
    public int Height { get; set; }
    public override int Area() => Width * Height;
}
```

### 32. How can you enforce encapsulation while allowing flexible access to object properties?  
- Use private fields with public properties for controlled access.  
- Leverage `get` and `set` accessors with logic validation.  
- Use access modifiers to restrict visibility.  
- Implement read-only properties for immutable values.  
- Example:  
```csharp
class Product {
    private decimal price;
    public decimal Price {
        get => price;
        set {
            if (value > 0) price = value;
        }
    }
}
```

### 33. What is the difference between abstract classes and interfaces? Provide examples in C#.  
- Abstract classes can have implementations; interfaces cannot.  
- A class can implement multiple interfaces but inherit only one abstract class.  
- Interfaces define behavior contracts; abstract classes provide shared behavior.  
- Abstract classes can have fields; interfaces cannot.  
- Example:  
```csharp
abstract class Animal {
    public abstract void Speak();
}
interface IFlyable {
    void Fly();
}
class Bird : Animal, IFlyable {
    public override void Speak() => Console.WriteLine("Chirp");
    public void Fly() => Console.WriteLine("Flying");
}
```

### 34. How do design patterns like Singleton and Factory adhere to OOP principles?  
- Singleton encapsulates the instance and provides controlled access (encapsulation, abstraction).  
- Factory abstracts object creation (abstraction, open/closed principle).  
- Promotes reusability and scalability.  
- Reduces code duplication and dependency coupling.  
- Example: A Singleton database connection or Factory for shape creation.  

```csharp
class Database {
    private static Database instance;
    private Database() {}
    public static Database Instance => instance ??= new Database();
}
```

### 35. How does the concept of dependency inversion lead to loosely coupled systems?  
- High-level modules should not depend on low-level modules; both should depend on abstractions.  
- Promotes reusability by decoupling concrete implementations.  
- Achieved using interfaces and dependency injection.  
- Simplifies testing by substituting mock implementations.  
- Example: Injecting a logging service into a class.  

```csharp
interface ILogger {
    void Log(string message);
}
class ConsoleLogger : ILogger {
    public void Log(string message) => Console.WriteLine(message);
}
class Application {
    private ILogger logger;
    public Application(ILogger logger) => this.logger = logger;
    public void Run() => logger.Log("App running");
}
```

### 36. Explain runtime polymorphism with examples in C#.  
- Achieved using method overriding with `virtual` and `override`.  
- Enables dynamic method dispatch at runtime.  
- Allows using base class references for derived class objects.  
- Useful for creating flexible and reusable code.  
- Example:  
```csharp
class Animal {
    public virtual void Speak() => Console.WriteLine("Animal sound");
}
class Dog : Animal {
    public override void Speak() => Console.WriteLine("Dog barks");
}
Animal animal = new Dog();
animal.Speak();  // Output: Dog barks
```

### 37. What are the benefits of using interfaces in OOP design?  
- Facilitates multiple inheritance by allowing a class to implement multiple interfaces.  
- Encourages loose coupling by relying on contracts rather than concrete classes.  
- Enhances flexibility and reusability in system design.  
- Simplifies testing by mocking implementations.  
- Example: I used an interface for database access to support both SQL and NoSQL in my project.  

```csharp
interface IDatabase {
    void Save(string data);
}
```

### 38. How does method overriding differ from method overloading?  
- Overloading: Same method name, different signatures in the same class.  
- Overriding: Redefining a base class method in a derived class.  
- Overloading is compile-time polymorphism; overriding is runtime polymorphism.  
- Overriding requires `virtual` and `override` keywords.  
- Example:  
```csharp
class Base {
    public virtual void Show() => Console.WriteLine("Base class");
}
class Derived : Base {
    public override void Show() => Console.WriteLine("Derived class");
}
```

### 39. What is an abstract property in C#?  
- A property declared in an abstract class without implementation.  
- Forces derived classes to provide implementation.  
- Allows abstraction of property behavior.  
- Ensures consistency across derived classes.  
- Example:  
```csharp
abstract class Shape {
    public abstract int Area { get; }
}
class Rectangle : Shape {
    public int Width { get; set; }
    public int Height { get; set; }
    public override int Area => Width * Height;
}
```

### 40. How does dependency injection promote better software design?  
- Decouples components by injecting dependencies rather than hardcoding them.  
- Improves testability with mock objects.  
- Enhances flexibility and scalability.  
- Implements the Dependency Inversion Principle.  
- Example: I used DI to manage services in a .NET Core web application.  

### 41. What is method hiding in C#?  
- Hides a base class method using the `new` keyword in a derived class.  
- Base class reference calls the base method, not the hidden method.  
- Does not affect runtime polymorphism.  
- Example:  
```csharp
class Base {
    public void Show() => Console.WriteLine("Base");
}
class Derived : Base {
    public new void Show() => Console.WriteLine("Derived");
}
```

### 42. Explain the use of the partial keyword in C#.  
- Splits a class or method into multiple files for better organization.  
- Allows collaborative development on large classes.  
- Combines all parts during compilation.  
- Example:  
```csharp
partial class Sample {
    public void Part1() => Console.WriteLine("Part 1");
}
partial class Sample {
    public void Part2() => Console.WriteLine("Part 2");
}
```

### 43. What is the purpose of the readonly keyword in C#?  
- Declares a field that can only be assigned during declaration or in the constructor.  
- Ensures immutability after initialization.  
- Useful for constants derived from runtime values.  
- Example:  
```csharp
class Example {
    public readonly int Value = 10;
    public Example(int value) {
        Value = value;
    }
}
```

### 44. How do delegates work in C#, and what are their benefits?  
- Delegates are type-safe function pointers.  
- Enable methods to be passed as parameters.  
- Support event handling and callback mechanisms.  
- Promote decoupling of methods from their invocation.  
- Example:  
```csharp
delegate void Notify(string message);
class Program {
    static void Main() {
        Notify notify = Console.WriteLine;
        notify("Hello, delegate!");
    }
}
```

### 45. What is the purpose of generics in C#?  
- Enable type-safe data structures and methods without specifying a concrete type.  
- Reduce code duplication by creating reusable components.  
- Improve performance by avoiding boxing and unboxing.  
- Example: I used generics to build a custom repository in a data access layer.  
```csharp
class GenericRepository<T> where T : class {
    public void Add(T entity) => Console.WriteLine($"Added {entity}");
}
```

Here are 15 new, unique questions and answers based on OOP and C#. These do not repeat any from the above list.  

### 1. What is the purpose of the `base` keyword in C#?  
- Allows access to members of the base class from a derived class.  
- Used to invoke base class constructors.  
- Enables overriding methods to extend base functionality.  
- Ensures derived class can reuse and enhance base class logic.  
- Example:  
```csharp
class Parent {
    public Parent(string message) => Console.WriteLine("Parent: " + message);
}
class Child : Parent {
    public Child(string message) : base(message) => Console.WriteLine("Child: " + message);
}
```

### 2. What are extension methods in C#?  
- Provide additional functionality to existing classes without modifying them.  
- Defined as static methods in static classes.  
- The first parameter specifies the type being extended and uses the `this` keyword.  
- Useful for enhancing third-party libraries or sealed classes.  
- Example:  
```csharp
public static class StringExtensions {
    public static int WordCount(this string str) => str.Split(' ').Length;
}
// Usage:
string text = "Hello world!";
Console.WriteLine(text.WordCount());
```

### 3. What are nullable types in C#, and why are they used?  
- Allow value types to represent null.  
- Declared using `T?` syntax (e.g., `int?`).  
- Useful for scenarios where absence of a value is meaningful.  
- Includes methods like `.HasValue` and `.Value`.  
- Example:  
```csharp
int? nullableInt = null;
if (nullableInt.HasValue) Console.WriteLine(nullableInt.Value);
```

### 4. What is the difference between `ref` and `out` keywords in C#?  
- Both pass parameters by reference, but with different requirements.  
- `ref`: The variable must be initialized before passing.  
- `out`: The variable does not need to be initialized before passing.  
- `out` ensures a value is assigned inside the method.  
- Example:  
```csharp
void Example(ref int a, out int b) {
    a += 1;
    b = 10;
}
int x = 5, y;
Example(ref x, out y);
Console.WriteLine(x);  // Output: 6
Console.WriteLine(y);  // Output: 10
```

### 5. What is the use of the `dynamic` keyword in C#?  
- Bypasses compile-time type checking for variables.  
- Type resolution happens at runtime.  
- Useful for scenarios involving reflection, COM objects, or dynamic languages.  
- Example:  
```csharp
dynamic value = 10;
Console.WriteLine(value.GetType()); // Output: System.Int32
value = "Hello";
Console.WriteLine(value.GetType()); // Output: System.String
```

### 6. What is the purpose of the `is` and `as` keywords in C#?  
- **`is`**: Checks if an object is compatible with a type.  
- **`as`**: Performs a type cast and returns null if the cast fails.  
- Avoids exceptions compared to traditional casting.  
- Example:  
```csharp
object obj = "Test";
if (obj is string str) Console.WriteLine(str);
string castedStr = obj as string;
Console.WriteLine(castedStr ?? "Not a string");
```

### 7. What is the purpose of the `yield` keyword in C#?  
- Facilitates stateful iteration in methods.  
- Used in conjunction with `IEnumerable` or `IEnumerator`.  
- Enables deferred execution for collection traversal.  
- Example:  
```csharp
IEnumerable<int> GetNumbers() {
    for (int i = 1; i <= 5; i++) yield return i;
}
// Usage:
foreach (var num in GetNumbers()) Console.WriteLine(num);
```

### 8. What is the purpose of `nameof` in C#?  
- Retrieves the name of a variable, property, or class as a string.  
- Prevents hardcoding and improves refactoring.  
- Useful for logging and exceptions.  
- Example:  
```csharp
string propertyName = nameof(Console.WriteLine);
Console.WriteLine(propertyName);  // Output: WriteLine
```

### 9. What is the difference between `Task` and `Thread` in C#?  
- **Task**: Higher-level abstraction for concurrent operations.  
- **Thread**: Represents a single, low-level OS thread.  
- Tasks allow easier cancellation, continuation, and exception handling.  
- Example:  
```csharp
Task.Run(() => Console.WriteLine("Task running"));
new Thread(() => Console.WriteLine("Thread running")).Start();
```

### 10. What are `indexers` in C#, and how are they implemented?  
- Allow objects to be indexed like arrays.  
- Use the `this` keyword with square brackets.  
- Simplify accessing collections within a class.  
- Example:  
```csharp
class Sample {
    private int[] numbers = new int[5];
    public int this[int index] {
        get => numbers[index];
        set => numbers[index] = value;
    }
}
// Usage:
Sample sample = new();
sample[0] = 42;
Console.WriteLine(sample[0]);
```

### 11. How does the `lock` keyword work in C#?  
- Prevents multiple threads from accessing a critical section simultaneously.  
- Ensures thread safety.  
- Used with an object reference as a lock token.  
- Example:  
```csharp
private readonly object lockObj = new();
void ThreadSafeMethod() {
    lock (lockObj) {
        Console.WriteLine("Thread-safe code");
    }
}
```

### 12. What is the purpose of `GC.Collect()` in C#?  
- Forces garbage collection to reclaim unused memory.  
- Should be used sparingly as it impacts performance.  
- Useful for testing or specific memory cleanup scenarios.  
- Example:  
```csharp
GC.Collect();
GC.WaitForPendingFinalizers();
```

### 13. What are tuples in C#, and when would you use them?  
- Lightweight structures for grouping multiple values.  
- Avoids creating custom types for simple data grouping.  
- Supports named elements for readability.  
- Example:  
```csharp
var tuple = (Id: 1, Name: "John");
Console.WriteLine(tuple.Name); // Output: John
```

### 14. How do events work in C#?  
- Encapsulate the publisher-subscriber pattern.  
- Subscribers register methods to execute when the event is raised.  
- Defined using the `event` keyword with delegates.  
- Example:  
```csharp
class Publisher {
    public event Action OnPublish;
    public void Publish() => OnPublish?.Invoke();
}
// Usage:
Publisher pub = new();
pub.OnPublish += () => Console.WriteLine("Event triggered");
pub.Publish();
```

### 15. What is the difference between `IEnumerable` and `IQueryable` in C#?  
- **IEnumerable**: Executes queries on the server; evaluates in memory.  
- **IQueryable**: Allows LINQ-to-SQL and deferred query execution on the database.  
- **IQueryable** is more efficient for large datasets.  
- Example:  
```csharp
IEnumerable<int> nums = new List<int> { 1, 2, 3 };
IQueryable<int> query = nums.AsQueryable();
```

