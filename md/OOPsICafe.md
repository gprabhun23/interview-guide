**1. What is inheritance?**  
- Inheritance is a feature of OOP that allows a class (child) to acquire properties and behaviors of another class (parent).  
- It helps in code reusability by enabling child classes to use existing parent class code.  
- Supports hierarchical relationships where a base class can have multiple derived classes.  
- Provides a way to override parent class methods for specific behaviors in the child class.  
- I used inheritance in my project to create a base service class for HTTP requests, which derived classes customized for specific APIs:  
```csharp
// Base Class
public class ApiService {
    public virtual void MakeRequest() {
        Console.WriteLine("Making API request");
    }
}

// Derived Class
public class UserService : ApiService {
    public override void MakeRequest() {
        Console.WriteLine("Making User API request");
    }
}
```  

**2. What is OOP?**  
- OOP (Object-Oriented Programming) is a programming paradigm that models concepts as "objects" with data and behavior.  
- It emphasizes modularity and reusability through encapsulation, inheritance, and polymorphism.  
- Encourages abstraction by hiding implementation details and exposing only relevant functionality.  
- Promotes easy maintenance and scalability for software development.  
- In one project, I structured an e-commerce application using OOP principles, such as encapsulating product data and providing services to handle shopping cart operations.  

**3. Why is the virtual keyword used in code?**  
- The `virtual` keyword allows a method, property, or event to be overridden in derived classes.  
- Ensures runtime polymorphism, enabling dynamic method binding based on the object type.  
- Helps in creating extensible systems by allowing behavior modifications in inherited classes.  
- Provides flexibility while maintaining a contract with the base class method signatures.  
- I used the `virtual` keyword in a .NET Core project to allow customizable logging behavior in derived logging services:  
```csharp
public class Logger {
    public virtual void Log(string message) {
        Console.WriteLine($"Log: {message}");
    }
}
public class FileLogger : Logger {
    public override void Log(string message) {
        System.IO.File.WriteAllText("log.txt", message);
    }
}
```  

**4. Difference between procedural and OOP?**  
- Procedural programming is task-oriented, focusing on functions and logic, while OOP is object-oriented, focusing on objects and their interactions.  
- Procedural uses a top-down approach, whereas OOP uses a bottom-up approach.  
- Data and functions are separate in procedural programming, but in OOP, they are encapsulated together.  
- Procedural programming lacks features like inheritance and polymorphism, which are central to OOP.  
- In a real-world example, I used procedural programming for simple scripts, like batch file processing, and OOP for larger applications like CRM systems for scalability and maintainability.  

**5. What is a class?**  
- A class is a blueprint for creating objects, defining data (fields) and behaviors (methods).  
- It encapsulates data for an object and provides methods for accessing and modifying it.  
- Classes enable abstraction by hiding complex implementation details from users.  
- They support OOP principles like inheritance and polymorphism.  
- In a project, I created a `Product` class to encapsulate product details for an inventory management system:  
```csharp
public class Product {
    public string Name { get; set; }
    public decimal Price { get; set; }
    
    public void DisplayInfo() {
        Console.WriteLine($"Product: {Name}, Price: {Price}");
    }
}
```

**6. Basic features of OOPs?**  
- Encapsulation: Bundles data and methods to restrict direct access to object components.  
- Inheritance: Allows a class to use properties and methods of another class.  
- Polymorphism: Enables objects to take on multiple forms based on context.  
- Abstraction: Hides implementation details, exposing only essential features.  
- I applied all these features while creating a hierarchical system for different types of reports in an analytics tool, ensuring extensibility and reusability.  

**7. Can you inherit private members of a class?**  
- Private members of a class cannot be directly inherited by derived classes.  
- Derived classes can only access public, protected, or internal members of the base class.  
- To indirectly use private members, the base class provides access through public or protected methods.  
- This ensures encapsulation, limiting access to sensitive data.  
- I followed this approach in a project by exposing private member data via protected methods for derived classes:  
```csharp
public class BaseClass {
    private string secret = "Hidden";

    protected string GetSecret() {
        return secret;
    }
}

public class DerivedClass : BaseClass {
    public void DisplaySecret() {
        Console.WriteLine(GetSecret());
    }
}
```

**8. What is the difference between a class and a structure?**  
- Classes are reference types, while structures are value types.  
- Classes support inheritance, but structures do not.  
- Structures are stored on the stack, while objects of classes are stored on the heap.  
- Example: I used a structure for a `Point` type in a graphics application for efficiency and a class for `Canvas` to manage complex operations.  

```csharp
struct Point {
    public int X { get; set; }
    public int Y { get; set; }
}

class Canvas {
    public Point Origin { get; set; }
}
```

**9. What is the relationship between a class and an object?**  
- A class is a blueprint or template, while an object is an instance of a class.  
- Classes define the structure and behavior, while objects store actual data and execute the behavior.  
- A class can create multiple objects, each with unique states.  
- Example: I designed a `User` class in a social media app, and objects represented individual users.  

```csharp
class User {
    public string Name { get; set; }
}

User user1 = new User { Name = "Alice" };
User user2 = new User { Name = "Bob" };
```

**10. What is an object bevel?**  
- The term "object bevel" seems unclear in the OOP context and may be misinterpreted.  
- Objects in OOP represent real-world entities with properties and methods.  
- It's important to clarify and use accurate terminology when discussing OOP concepts.  
- Example: If you meant "object behavior," I implemented an object's behavior like methods in a game where `Player` objects have `Jump` actions.  

```csharp
class Player {
    public void Jump() => Console.WriteLine("Player jumped");
}
Player player = new Player();
player.Jump();
```

**11. Explain the concept of a constructor.**  
- A constructor is a special method used to initialize an object when it is created.  
- It shares the same name as the class and has no return type.  
- Constructors can be parameterized or default, enabling object initialization flexibility.  
- Example: I used a constructor in a `Product` class to set initial values for name and price in an e-commerce app.  

```csharp
class Product {
    public string Name { get; }
    public decimal Price { get; }

    public Product(string name, decimal price) {
        Name = name;
        Price = price;
    }
}

Product product = new Product("Laptop", 1200.00m);
```

**12. What is Encapsulation?**  
- Encapsulation is the practice of bundling data and methods into a single unit (class).  
- It restricts direct access to some components and protects the object's integrity.  
- Access modifiers like `private`, `public`, and `protected` enforce encapsulation.  
- Example: In a banking app, I encapsulated account details to prevent unauthorized access and used getters/setters for controlled access.  

```csharp
class BankAccount {
    private decimal balance;
    public decimal GetBalance() => balance;
    public void Deposit(decimal amount) => balance += amount;
}
```

**13. What is Polymorphism?**  
- Polymorphism allows methods to take multiple forms (e.g., overriding, overloading).  
- It enables objects to interact through a common interface, promoting flexibility.  
- There are two types: compile-time (overloading) and runtime (overriding).  
- Example: In a zoo app, polymorphism let me create an `Animal` base class and override a `Speak` method in derived classes like `Dog` and `Cat`.  

```csharp
class Animal {
    public virtual void Speak() => Console.WriteLine("Animal speaks");
}

class Dog : Animal {
    public override void Speak() => Console.WriteLine("Woof");
}
Animal myDog = new Dog();
myDog.Speak();
```

**14. How could you define Abstraction in OOP?**  
- Abstraction hides the implementation details and exposes only the necessary functionalities.  
- It simplifies complex systems by reducing the visible complexity to the user.  
- Abstract classes and interfaces are used to achieve abstraction.  
- Example: In a vehicle system, I used an abstract `Vehicle` class to define common methods like `Start` and `Stop` without showing internal engine details.  

```csharp
abstract class Vehicle {
    public abstract void Start();
    public abstract void Stop();
}

class Car : Vehicle {
    public override void Start() => Console.WriteLine("Car started");
    public override void Stop() => Console.WriteLine("Car stopped");
}
Vehicle myCar = new Car();
myCar.Start();
```

**15. How can you prevent your class from being inherited further?**  
- Use the `sealed` keyword to prevent a class from being inherited.  
- Sealing classes ensures no modifications or extensions can be made via inheritance.  
- It can be helpful when designing security-critical or immutable classes.  
- Example: I used a sealed class for `LicenseKeyManager` to ensure no one could alter its behavior.  

```csharp
sealed class LicenseKeyManager {
    public string GenerateKey() => "ABC123";
}

// Attempting to inherit this class will result in a compilation error.
```

**16. What do you mean by Data Encapsulation?**  
- Data encapsulation is the bundling of data and methods that operate on the data into a single unit (class).  
- It restricts direct access to an object's data, providing controlled access through methods or properties.  
- This ensures that an object's internal state is protected and can only be modified in intended ways.  
- Example: In a payroll system, I encapsulated employee details to ensure only authorized methods could modify salary information.  

```csharp
class Employee {
    private decimal salary;

    public decimal GetSalary() => salary;
    public void SetSalary(decimal value) {
        if (value > 0) salary = value;
    }
}
```

**17. What's the difference between a method and a function in OOP context?**  
- In OOP, a method is a function that is defined inside a class and operates on its objects.  
- Functions are independent and can exist outside of a class, while methods are inherently tied to their class or object.  
- Methods typically operate on instance data or class-level data, while functions are general-purpose.  
- Example: In a game, I used a `CalculateScore` method tied to the `Player` class instead of a standalone function for better modularity.  

```csharp
class Player {
    public int Score { get; set; }
    public void CalculateScore(int points) => Score += points;
}
```

**18. Can you specify the accessibility modifier for methods inside an interface?**  
- Methods in an interface are implicitly public and cannot have any other accessibility modifier.  
- This ensures that all implementing classes provide a public implementation of the methods.  
- Starting from C# 8.0, default interface methods allow implementation within interfaces but are still public by default.  
- Example: I created an `ILogger` interface with public methods to enforce consistent logging behavior across classes.  

```csharp
interface ILogger {
    void Log(string message);
}

class ConsoleLogger : ILogger {
    public void Log(string message) => Console.WriteLine(message);
}
```

**19. Is it possible for a class to inherit the constructor of its base class?**  
- Constructors are not inherited in C#. However, a derived class can call the base class constructor using `base`.  
- This ensures proper initialization of the base class when a derived class is instantiated.  
- Overriding constructors is done by explicitly defining them in the derived class.  
- Example: In a banking app, I used the base class constructor to initialize account properties in derived classes.  

```csharp
class Account {
    public Account(string accountHolder) => Console.WriteLine($"Account created for {accountHolder}");
}

class SavingsAccount : Account {
    public SavingsAccount(string accountHolder) : base(accountHolder) { }
}
SavingsAccount sa = new SavingsAccount("John");
```

**20. What are the similarities between a class and a structure?**  
- Both classes and structures can contain methods, properties, fields, and constructors.  
- Both can implement interfaces to enforce certain behaviors.  
- Both support access modifiers for encapsulating data.  
- Example: I used a structure for `Point` and a class for `Shape` in a graphics tool, as both shared similar members like properties for coordinates.  

```csharp
struct Point {
    public int X { get; set; }
    public int Y { get; set; }
}
class Shape {
    public string Name { get; set; }
}
```

**21. What are the different ways a method can be overloaded?**  
- By changing the number of parameters.  
- By altering the type of parameters.  
- By changing the order of parameters (only if types differ).  
- Example: I implemented overloaded methods in a calculator class to handle different data types like integers and doubles.  

```csharp
class Calculator {
    public int Add(int a, int b) => a + b;
    public double Add(double a, double b) => a + b;
}
Calculator calc = new Calculator();
Console.WriteLine(calc.Add(5, 10));
Console.WriteLine(calc.Add(5.5, 10.5));
```

**22. Interface or an Abstract class: which one to use?**  
- Use an interface to define a contract when multiple classes need to share common functionality but are unrelated.  
- Use an abstract class when classes share a common base and some implementation.  
- Abstract classes can have constructors and fields, but interfaces cannot.  
- Example: I used an interface `IMovable` for vehicles and animals, and an abstract class `Vehicle` for shared vehicle properties.  

```csharp
interface IMovable {
    void Move();
}

abstract class Vehicle : IMovable {
    public abstract void Move();
}
```

**23. What is the Unit of Work pattern?**  
- The Unit of Work pattern maintains a list of changes to be made and coordinates their execution as a single unit.  
- It helps manage transactions by ensuring all operations either succeed or fail together.  
- Commonly used with the Repository pattern in data persistence layers.  
- Example: In an e-commerce app, I used Unit of Work to save orders and update inventory in a single transaction.  

**24. What is the difference between an Interface and an Abstract Class?**  
- An interface only declares methods and properties, while an abstract class can provide implementations.  
- Abstract classes can have fields and constructors; interfaces cannot.  
- A class can implement multiple interfaces but inherit only one abstract class.  
- Example: I used interfaces for cross-cutting concerns like logging, and an abstract class for shared vehicle functionality.  

```csharp
abstract class Vehicle {
    public abstract void Drive();
}
interface ILogger {
    void Log(string message);
}
```

**25. How can you prevent a class from overriding methods in C#?**  
- Use the `sealed` keyword with a method to prevent it from being overridden in derived classes.  
- Sealed methods must be declared in classes that are not sealed themselves.  
- This ensures no further modifications to the method's behavior.  
- Example: I sealed the `ProcessOrder` method in an order management system to enforce standard behavior.  

```csharp
class Order {
    public virtual void ProcessOrder() => Console.WriteLine("Processing order");
}

class SpecialOrder : Order {
    public sealed override void ProcessOrder() => Console.WriteLine("Processing special order");
}
```
**26. What is the difference between a Virtual method and an Abstract method?**  
- A virtual method has a default implementation, while an abstract method does not and must be overridden.  
- Virtual methods can be optionally overridden in derived classes; abstract methods must be implemented.  
- Virtual methods are declared in non-abstract classes, whereas abstract methods are only in abstract classes.  
- Example: In a file management app, I used a virtual `OpenFile` method with a default implementation and an abstract `ParseFile` method for specific file types.  

```csharp
abstract class File {
    public virtual void OpenFile() => Console.WriteLine("Opening file");
    public abstract void ParseFile();
}

class TextFile : File {
    public override void ParseFile() => Console.WriteLine("Parsing text file");
}
```

**27. When should I use a struct instead of a class?**  
- Use a struct for lightweight objects that represent a single value or small group of related values.  
- Structs are ideal when immutability and value-type behavior are required.  
- Structs avoid heap allocation, making them more efficient for small, frequently used objects.  
- Example: I used a `Point` struct in a graphics library for efficient manipulation of 2D coordinates.  

```csharp
struct Point {
    public int X { get; set; }
    public int Y { get; set; }
}
Point p = new Point { X = 5, Y = 10 };
```

**28. What is Polymorphism, what is it for, and how is it used?**  
- Polymorphism allows objects to be treated as instances of their base type, enabling code generalization.  
- It promotes flexibility and extensibility in systems.  
- Polymorphism is implemented through method overriding or interfaces.  
- Example: I used polymorphism in a payment gateway to handle various payment methods (`CreditCard`, `PayPal`) using a common interface.  

```csharp
interface IPayment {
    void ProcessPayment();
}

class CreditCardPayment : IPayment {
    public void ProcessPayment() => Console.WriteLine("Processing credit card payment");
}
IPayment payment = new CreditCardPayment();
payment.ProcessPayment();
```

**29. What are abstract classes? What are the distinct characteristics of an abstract class?**  
- Abstract classes cannot be instantiated and are designed to be inherited.  
- They may contain abstract methods (without implementation) and concrete methods (with implementation).  
- Abstract classes are used to define shared functionality while enforcing implementation in derived classes.  
- Example: I used an abstract class `Shape` in a drawing application to define a `Draw` method that was implemented differently for `Circle` and `Rectangle`.  

```csharp
abstract class Shape {
    public abstract void Draw();
}
class Circle : Shape {
    public override void Draw() => Console.WriteLine("Drawing Circle");
}
```

**30. State the features of an Interface.**  
- An interface defines a contract with no implementation.  
- It supports multiple inheritance and allows classes to implement multiple interfaces.  
- Interfaces cannot contain fields or constructors, only methods, properties, and events.  
- Example: I used an interface `ISerializable` in a data export module to enforce a standard serialization method across classes.  

```csharp
interface ISerializable {
    string Serialize();
}
class Product : ISerializable {
    public string Serialize() => "Product data serialized";
}
```

**31. How is method overriding different from method overloading?**  
- Overriding changes the behavior of a method in a derived class, while overloading provides multiple methods with the same name but different parameters.  
- Overriding is achieved using `virtual` and `override` keywords; overloading doesn't require special keywords.  
- Overriding is a runtime mechanism, while overloading is a compile-time mechanism.  
- Example: I used overriding in a base class `Animal` to modify the `Speak` method in derived classes and overloading in a `Calculator` for adding integers and doubles.  

```csharp
// Overriding
class Animal {
    public virtual void Speak() => Console.WriteLine("Animal speaks");
}
class Dog : Animal {
    public override void Speak() => Console.WriteLine("Dog barks");
}

// Overloading
class Calculator {
    public int Add(int a, int b) => a + b;
    public double Add(double a, double b) => a + b;
}
```

**32. What is a static constructor?**  
- A static constructor initializes static data or performs actions that only need to be done once for a class.  
- It is called automatically before any instance is created or static members are accessed.  
- It has no access modifiers and takes no parameters.  
- Example: I used a static constructor in a configuration manager class to load settings once when the application started.  

```csharp
class ConfigManager {
    static ConfigManager() {
        Console.WriteLine("Loading configuration...");
    }
}
```

**33. What exactly is the difference between an Interface and an Abstract class?**  
- Abstract classes can have concrete implementations; interfaces cannot (pre-C# 8.0).  
- A class can inherit from one abstract class but implement multiple interfaces.  
- Abstract classes can define fields and constructors; interfaces cannot.  
- Example: I used an abstract class for shared properties in a report system and interfaces for behavior like `IPrintable`.  

**34. Differentiate between an abstract class and an interface.**  
- Abstract classes provide partial implementation, while interfaces provide no implementation.  
- Abstract classes can contain non-public members; interfaces cannot.  
- Interfaces support multiple inheritance, whereas abstract classes do not.  
- Example: I used an interface for `ILogging` to enforce logging and an abstract class `Device` to share common device properties.  

```csharp
abstract class Device {
    public string Name { get; set; }
}
interface ILogging {
    void Log(string message);
}
```

**35. Does .NET support multiple inheritance?**  
- .NET does not support multiple inheritance with classes but allows it with interfaces.  
- This prevents ambiguity in inheriting members from multiple base classes.  
- Mixins or interface combinations are used to achieve similar functionality.  
- Example: I implemented multiple interfaces like `IMovable` and `IDrawable` in a game object.  

```csharp
interface IMovable {
    void Move();
}
interface IDrawable {
    void Draw();
}
class GameObject : IMovable, IDrawable {
    public void Move() => Console.WriteLine("Moving object");
    public void Draw() => Console.WriteLine("Drawing object");
}
```

**36. What is Coupling in OOP?**  
- Coupling refers to the degree of dependency between different modules or classes in a program.  
- Tight coupling occurs when classes are heavily dependent on each other, making the code less flexible.  
- Loose coupling ensures minimal dependencies, leading to easier maintenance and scalability.  
- Example: I used dependency injection to achieve loose coupling in a web application by injecting services like `ILogger` into controllers.  

```csharp
class Controller {
    private readonly ILogger _logger;

    public Controller(ILogger logger) {
        _logger = logger;
    }

    public void Execute() => _logger.Log("Executing action");
}
```

**37. What is the difference between an abstract function and a virtual function?**  
- Abstract functions have no implementation and must be overridden in derived classes.  
- Virtual functions have a default implementation that can be optionally overridden.  
- Abstract functions are declared in abstract classes, whereas virtual functions can be in any class.  
- Example: I used an abstract function `Draw` in a `Shape` class and a virtual function `Display` with default behavior.  

```csharp
abstract class Shape {
    public abstract void Draw();
}

class Circle : Shape {
    public override void Draw() => Console.WriteLine("Drawing Circle");
}
```

**38. What is Cohesion in OOP?**  
- Cohesion refers to how closely related and focused the responsibilities of a single module or class are.  
- High cohesion indicates that a class or module has a single, well-defined responsibility.  
- Low cohesion can make a class harder to maintain and understand.  
- Example: I designed a `ReportGenerator` class solely for generating reports, keeping responsibilities focused and cohesive.  

```csharp
class ReportGenerator {
    public void GenerateReport() => Console.WriteLine("Generating Report");
}
```

**39. Can you declare an overridden method to be static if the original method is not static?**  
- No, in C#, the modifier of the overridden method must match the original method's signature.  
- A non-static method cannot be overridden as static, and vice versa.  
- This ensures consistent behavior when invoking the method through a base class reference.  
- Example: I maintained consistency by overriding non-static methods for polymorphic behavior in a user management system.  

```csharp
class User {
    public virtual void Login() => Console.WriteLine("User login");
}

class Admin : User {
    public override void Login() => Console.WriteLine("Admin login");
}
```

**40. Could you explain some benefits of the Repository Pattern?**  
- The Repository Pattern abstracts the data access layer, providing a clean separation between business logic and data logic.  
- It centralizes data access logic, making it reusable and easier to manage.  
- It enables better testing by allowing mocking of the repository layer.  
- Example: I implemented a `UserRepository` in a social networking app to manage user data interactions.  

```csharp
interface IUserRepository {
    User GetUserById(int id);
}
class UserRepository : IUserRepository {
    public User GetUserById(int id) => new User { Id = id, Name = "Sample User" };
}
```

**41. Explain the concept of Destructor.**  
- A destructor is used to release unmanaged resources held by an object before it is destroyed.  
- In C#, destructors are declared using a tilde (~) followed by the class name.  
- Destructors are automatically invoked and cannot be explicitly called.  
- Example: I used a destructor in a `FileHandler` class to close file streams automatically when objects were no longer needed.  

```csharp
class FileHandler {
    ~FileHandler() => Console.WriteLine("FileHandler destructor called");
}
```

**42. Explain different types of inheritance.**  
- **Single Inheritance**: A class inherits from one base class.  
- **Multiple Inheritance**: A class inherits from multiple base classes (not supported directly in C#, but achievable through interfaces).  
- **Multilevel Inheritance**: A class inherits from a class, which itself inherits from another class.  
- **Hierarchical Inheritance**: Multiple classes inherit from a single base class.  
- Example: I used hierarchical inheritance in an HR system where `Employee` was a base class, and `Manager` and `Technician` derived from it.  

```csharp
class Employee { }
class Manager : Employee { }
class Technician : Employee { }
```

**43. What's the advantage of using getters and setters instead of simply using public fields?**  
- Getters and setters provide controlled access to fields, allowing validation or logic during data access.  
- They help maintain encapsulation, keeping the internal state protected.  
- Fields can be modified to properties without affecting external code.  
- Example: I used a setter in a `User` class to validate email addresses before assignment.  

```csharp
class User {
    private string email;
    public string Email {
        get => email;
        set {
            if (value.Contains("@")) email = value;
        }
    }
}
```

**44. How to solve Circular Reference?**  
- Avoid circular dependencies by redesigning relationships between classes or introducing interfaces.  
- Use dependency injection to decouple classes.  
- Consider breaking circular references by using events or callbacks.  
- Example: I resolved a circular reference between `Order` and `Customer` classes by introducing an `ICustomer` interface.  

```csharp
interface ICustomer { }
class Customer : ICustomer { }
class Order {
    private ICustomer customer;
    public Order(ICustomer customer) => this.customer = customer;
}
```

**45. When should I use an Interface and when should I use a Base Class?**  
- Use an interface for defining contracts when unrelated classes share common behavior.  
- Use a base class when classes share common implementation or a logical hierarchy.  
- Interfaces support multiple inheritance; base classes do not.  
- Example: I used an interface `IDrawable` for rendering, and a base class `Shape` for shared geometry properties.  

```csharp
interface IDrawable {
    void Draw();
}
abstract class Shape : IDrawable {
    public abstract void Draw();
}
```

**46. What is the difference between Cohesion and Coupling?**  
- Cohesion refers to how focused a class/module is on a single responsibility.  
- Coupling refers to the level of dependency between classes/modules.  
- High cohesion and low coupling are desired for maintainable and scalable code.  
- Example: I achieved high cohesion by separating `Invoice` generation and email sending into distinct classes, reducing coupling through dependency injection.  

**47. What is the difference between Association, Aggregation, and Composition?**  
- **Association**: A general relationship between two classes, such as teacher and student.  
- **Aggregation**: A "has-a" relationship where one class contains another, but they can exist independently.  
- **Composition**: A stronger "has-a" relationship where the contained object cannot exist without the container.  
- Example: I used aggregation for `Team` and `Player` objects and composition for `Car` and `Engine`.  

```csharp
class Engine { }
class Car {
    private Engine engine = new Engine();
}
```

**48. Why doesn't C# allow static methods to implement an interface?**  
- Static methods are not tied to an instance, while interface methods are meant to be instance-level contracts.  
- Allowing static methods in interfaces would violate the instance-based design of interfaces.  
- Example: Instead of static methods, I used instance methods in the `ILogger` interface for logging functionality.  

**49. Can you provide a simple explanation of methods vs. functions in OOP context?**  
- A method is a function defined within a class and operates on its instance or class data.  
- Functions are general and can exist outside of a class.  
- Methods are context-specific to objects, while functions are context-independent.  
- Example: I used methods like `CalculateScore` in a `Player` class tied to the object instance.  

```csharp
class Player {
    public int Score { get; set; }
    public void CalculateScore(int points) => Score += points;
}
```

**50. Can you declare a private class in a namespace?**  
- No, classes declared directly in a namespace cannot have the `private` modifier.  
- Classes within another class (nested classes) can be private.  
- Example: I used a private nested class in a `CacheManager` for internal caching logic.  

```csharp
class CacheManager {
    private class CacheItem {
        public string Key { get; set; }
    }
}
```  

**51. Could you elaborate on Polymorphism, Overriding, and Overloading?**  
- **Polymorphism** allows the same operation to behave differently on different classes, supporting runtime flexibility.  
- **Overriding** occurs when a derived class provides a new implementation for a virtual/abstract method from the base class.  
- **Overloading** allows multiple methods in the same class with the same name but different parameters.  
- Example: I used overriding in a `PaymentProcessor` to define `ProcessPayment` differently for `CreditCard` and `PayPal` classes, and overloading for logging messages.  

```csharp
class PaymentProcessor {
    public virtual void ProcessPayment() => Console.WriteLine("Processing payment");
}
class CreditCardProcessor : PaymentProcessor {
    public override void ProcessPayment() => Console.WriteLine("Processing credit card payment");
}
```

**52. Why is a destructor in C# not executing?**  
- The garbage collector calls destructors, and execution timing isn't guaranteed.  
- If the application ends before the garbage collector runs, the destructor might not execute.  
- Explicit resource cleanup should use `IDisposable` and `using` blocks instead.  
- Example: I implemented `IDisposable` in a file manager to ensure resource cleanup instead of relying on destructors.  

```csharp
class FileManager : IDisposable {
    public void Dispose() => Console.WriteLine("Releasing resources");
}
```

**53. What is the difference between Mixins and Inheritance?**  
- Mixins provide reusable functionality through composition, often via interfaces or abstract classes.  
- Inheritance is a hierarchical relationship between base and derived classes.  
- Mixins allow combining behaviors from multiple sources; inheritance allows sharing structure and behavior from a single source.  
- Example: I implemented mixins in a logging system by combining `ILogger` and `IFormatter` interfaces.  

```csharp
interface ILogger {
    void Log(string message);
}
interface IFormatter {
    string Format(string message);
}
class ConsoleLogger : ILogger, IFormatter {
    public void Log(string message) => Console.WriteLine(Format(message));
    public string Format(string message) => $"[LOG]: {message}";
}
```

**54. What is LSP (Liskov Substitution Principle) and what are some examples of its use?**  
- LSP states that objects of a superclass should be replaceable with objects of a subclass without affecting the program.  
- It ensures derived classes enhance, not modify or restrict, base class behavior.  
- Violations occur when a subclass breaks expected behavior of the base class.  
- Example: I applied LSP in a payment module, ensuring all payment types derived from a common `Payment` class adhered to shared behavior.  

```csharp
abstract class Payment {
    public abstract void Process();
}
class CreditCardPayment : Payment {
    public override void Process() => Console.WriteLine("Processing Credit Card Payment");
}
Payment payment = new CreditCardPayment();
payment.Process(); // Works as expected
```

**55. In terms that an OOP programmer would understand, what is a Monad?**  
- A Monad is a design pattern used to handle data transformations and chaining operations while maintaining context.  
- It is commonly used in functional programming but is adaptable to OOP concepts.  
- Monads ensure that operations handle additional concerns like nullability, errors, or side effects.  
- Example: In a banking app, I used a Monad-like approach to handle safe chaining of nullable objects.  

```csharp
public class Maybe<T> {
    private readonly T _value;
    public Maybe(T value) => _value = value;
    public TResult Bind<TResult>(Func<T, TResult> func) => _value != null ? func(_value) : default;
}
```

**56. Why prefer Composition over Inheritance? What trade-offs are there for each approach?**  
- Composition promotes flexibility by combining behaviors dynamically rather than relying on static hierarchies.  
- It avoids the tight coupling and fragility of deep inheritance trees.  
- Inheritance is simpler for shared behavior in strongly related classes.  
- Example: I used composition in a plugin system, combining `IRenderer` and `IExporter` for modular functionality.  

```csharp
interface IRenderer { void Render(); }
interface IExporter { void Export(); }
class Plugin : IRenderer, IExporter {
    public void Render() => Console.WriteLine("Rendering...");
    public void Export() => Console.WriteLine("Exporting...");
}
```

**57. What does it mean to program to an Interface?**  
- Programming to an interface means depending on abstractions rather than concrete implementations.  
- It promotes flexibility and enables easy swapping of implementations.  
- This approach aligns with the Dependency Inversion Principle.  
- Example: I designed a payment system by programming to the `IPayment` interface, allowing easy addition of new payment methods.  

```csharp
interface IPayment {
    void ProcessPayment();
}
class CreditCardPayment : IPayment {
    public void ProcessPayment() => Console.WriteLine("Credit Card Payment Processed");
}
```
