**1. What are the main categories of design patterns?**  
- Creational patterns deal with object creation mechanisms, enhancing flexibility and reuse.  
- Structural patterns focus on object composition, simplifying relationships between entities.  
- Behavioral patterns address object collaboration and responsibility delegation.  
- Examples include Singleton (Creational), Adapter (Structural), and Observer (Behavioral).  
- I used Behavioral patterns in an event-driven project to manage communication between objects using the Observer pattern. Example:  

```csharp
public class ObserverExample
{
    public interface IObserver { void Update(string message); }
    public class Subject
    {
        private List<IObserver> observers = new List<IObserver>();
        public void AddObserver(IObserver observer) => observers.Add(observer);
        public void NotifyObservers(string message)
        {
            observers.ForEach(o => o.Update(message));
        }
    }
}
```

---

**2. What is a design pattern and why should anyone use them?**  
- A design pattern is a proven, reusable solution to a common software design problem.  
- They improve communication by providing shared terminology.  
- Using them promotes code reusability, scalability, and maintainability.  
- In my .NET Core API project, Singleton ensured a single instance of a logger, optimizing resource usage. Example:  

```csharp
public sealed class Logger
{
    private static readonly Logger instance = new Logger();
    private Logger() {}
    public static Logger Instance => instance;
    public void Log(string message) { Console.WriteLine(message); }
}
```

---

**3. What is a pattern in software design?**  
- A pattern is a general reusable solution to a recurring problem.  
- It’s not a finished design but a template for solving problems.  
- Patterns guide developers to write optimized and clean code.  
- In an Angular project, I used patterns to structure reusable services and components effectively.  

---

**4. What is the Singleton design pattern?**  
- Ensures only one instance of a class exists throughout the application.  
- Provides a global point of access to that instance.  
- It is useful for managing shared resources like configuration or logging.  
- Implemented Singleton for database connections in my project, reducing overhead. Example:  

```csharp
public sealed class DatabaseConnection
{
    private static readonly DatabaseConnection instance = new DatabaseConnection();
    private DatabaseConnection() { }
    public static DatabaseConnection Instance => instance;
}
```

---

**5. What is Dependency Injection?**  
- A technique to achieve Inversion of Control by providing dependencies externally.  
- It decouples the creation of an object from its usage.  
- Promotes testability and easier maintenance.  
- Used Dependency Injection in .NET Core using built-in support to inject services into controllers. Example:  

```csharp
public class MyService : IMyService
{
    public void Execute() { /* Implementation */ }
}
```

---

**6. What is the State design pattern?**  
- Allows an object to alter its behavior when its internal state changes.  
- Encapsulates state-specific behavior in separate classes.  
- Improves code organization and makes it easy to add new states.  
- Implemented this pattern for managing payment statuses in an e-commerce application. Example:  

```csharp
public interface IState { void Handle(); }
public class ApprovedState : IState { public void Handle() { Console.WriteLine("Payment approved."); } }
public class RejectedState : IState { public void Handle() { Console.WriteLine("Payment rejected."); } }
```

---

**7. What is the Null Object pattern?**  
- Provides a default implementation for a class to avoid null checks.  
- Improves code readability and reduces null reference errors.  
- Useful for cases where the absence of an object should be handled gracefully.  
- Used this pattern to avoid null checks in optional service handling. Example:  

```csharp
public interface IService { void Execute(); }
public class NullService : IService { public void Execute() { } }
```

---

**8. What is the Template Method pattern?**  
- Defines the skeleton of an algorithm in a method, deferring some steps to subclasses.  
- Promotes code reuse and flexibility.  
- Useful in situations with a common sequence of steps but variation in certain steps.  
- Applied in a report generation system where formatting differed by report type. Example:  

```csharp
public abstract class ReportTemplate
{
    public void GenerateReport() { FetchData(); FormatReport(); SaveReport(); }
    protected abstract void FetchData();
    protected abstract void FormatReport();
    protected void SaveReport() { Console.WriteLine("Saving Report..."); }
}
```

---

**9. What is the Iterator pattern?**  
- Provides a way to access elements of a collection sequentially without exposing its structure.  
- Useful for traversing complex data structures.  
- Promotes encapsulation and simplifies traversal.  
- Used this pattern for custom collections in a financial app. Example:  

```csharp
public interface IIterator { bool HasNext(); object Next(); }
public class ArrayIterator : IIterator
{
    private int[] _array;
    private int position = 0;
    public ArrayIterator(int[] array) { _array = array; }
    public bool HasNext() => position < _array.Length;
    public object Next() => _array[position++];
}
```

---

**10. What is the Strategy pattern?**  
- Defines a family of algorithms and makes them interchangeable.  
- Promotes flexibility and reduces conditional logic.  
- Ideal for implementing various behaviors dynamically.  
- Used for implementing sorting algorithms in a library system. Example:  

```csharp
public interface ISortingStrategy { void Sort(int[] data); }
public class QuickSort : ISortingStrategy { public void Sort(int[] data) { /* QuickSort implementation */ } }
```

---

**11. What is the Proxy pattern?**  
- Provides a surrogate or placeholder for another object to control access.  
- Useful for lazy initialization, logging, or security purposes.  
- Reduces resource usage by controlling object creation.  
- Used a Proxy for caching API responses in a project. Example:  

```csharp
public class ServiceProxy : IService
{
    private RealService _realService;
    public void Execute()
    {
        if (_realService == null) _realService = new RealService();
        _realService.Execute();
    }
}
```

---

**12. What are some benefits of the Repository pattern?**  
- Centralizes data access logic, improving code maintainability.  
- Abstracts database operations, making code database-agnostic.  
- Simplifies testing by enabling mock repositories.  
- Used in a Unit of Work setup for efficient transaction management. Example:  

```csharp
public interface IRepository<T> { T GetById(int id); void Add(T entity); }
public class Repository<T> : IRepository<T> { /* Implementation */ }
```

---

**13. What is the Filter pattern?**  
- Filters a set of objects using different criteria and chaining them together.  
- Promotes flexibility and reusability.  
- Useful in applications requiring dynamic filtering.  
- Implemented in a product filtering module of an e-commerce site. Example:  

```csharp
public interface IFilter<T> { IEnumerable<T> Filter(IEnumerable<T> items); }
```

---

**14. What is the Builder pattern?**  
- Separates object construction from its representation.  
- Ideal for creating complex objects with multiple configurations.  
- Simplifies object creation and promotes immutability.  
- Used for building configuration files dynamically. Example:  

```csharp
public class ProductBuilder { public ProductBuilder SetName(string name) { /* Implementation */ return this; } }
```

---

**15. What are the types of design patterns?**  
- Creational patterns focus on object creation.  
- Structural patterns emphasize object relationships and compositions.  
- Behavioral patterns govern object collaboration and interactions.  
- Patterns like Singleton, Adapter, and Strategy cover these categories comprehensively.  
- Implemented Strategy for configurable export formats in a document processing system. Example:  

```csharp
public interface IExportStrategy { void Export(string data); }
public class PDFExport : IExportStrategy { public void Export(string data) { /* Export to PDF */ } }
```

**16. What is Inversion of Control?**  
- A design principle where the control of object creation and flow is transferred from the program to a framework or container.  
- Helps decouple the code by abstracting dependencies.  
- Implemented using Dependency Injection, Service Locators, or Events.  
- In .NET Core, IoC is achieved through the built-in Dependency Injection container. Example:  

```csharp
services.AddTransient<IMyService, MyService>();
```

---

**17. Why would you want to use a Repository pattern with an ORM?**  
- Abstracts database queries, allowing switching ORMs without changing business logic.  
- Simplifies testing by mocking repositories instead of actual database interactions.  
- Centralizes and organizes data access logic.  
- Used with Entity Framework Core to simplify queries and CRUD operations. Example:  

```csharp
public class ProductRepository : IRepository<Product>
{
    private readonly DbContext _context;
    public ProductRepository(DbContext context) { _context = context; }
    public Product GetById(int id) => _context.Products.Find(id);
}
```

---

**18. Can we create a clone of a Singleton object?**  
- Technically, it is possible but violates the Singleton principle.  
- Using reflection or serialization can bypass Singleton constraints.  
- This is generally discouraged as it defeats the purpose of Singleton.  
- Prevented cloning in a project by implementing `ICloneable` and throwing an exception. Example:  

```csharp
public class Singleton : ICloneable
{
    private static Singleton instance = new Singleton();
    private Singleton() { }
    public static Singleton Instance => instance;
    public object Clone() => throw new NotSupportedException("Cloning not allowed.");
}
```

---

**19. What is the Factory pattern?**  
- A creational pattern that provides an interface for creating objects without specifying their exact class.  
- Promotes loose coupling and enhances code flexibility.  
- Used for creating instances based on runtime conditions.  
- Implemented for a notification system to generate email or SMS services dynamically. Example:  

```csharp
public interface INotification { void Send(string message); }
public class NotificationFactory
{
    public INotification CreateNotification(string type) => type switch
    {
        "Email" => new EmailNotification(),
        "SMS" => new SmsNotification(),
        _ => throw new ArgumentException("Invalid type")
    };
}
```

---

**20. What is Unit of Work?**  
- A design pattern that groups related operations into a single transaction.  
- Ensures that all operations either succeed or fail together.  
- Works with Repository to manage object changes efficiently.  
- Used in my project to wrap multiple database operations in a transaction. Example:  

```csharp
public interface IUnitOfWork { void Commit(); }
public class UnitOfWork : IUnitOfWork
{
    private readonly DbContext _context;
    public UnitOfWork(DbContext context) { _context = context; }
    public void Commit() { _context.SaveChanges(); }
}
```

---

**21. What is the Claim Check pattern in Azure Event Grid?**  
- A messaging pattern to offload payloads from messages and replace them with references (claims).  
- Reduces message size, improving performance and scalability.  
- Claims are used to retrieve the full payload from storage when needed.  
- Used this to handle large messages efficiently in a distributed system. Example:  

```json
{
    "eventType": "PayloadReference",
    "data": {
        "url": "https://storage.blob.core.windows.net/container/message.json"
    }
}
```

---

**22. What is the Chain of Responsibility pattern?**  
- Passes a request along a chain of handlers until one processes it.  
- Decouples sender and receiver, promoting flexibility.  
- Useful for workflows or dynamic request processing.  
- Implemented for dynamic request validation in an API project. Example:  

```csharp
public abstract class Handler
{
    protected Handler Next;
    public void SetNext(Handler next) => Next = next;
    public abstract void HandleRequest(int request);
}
```

---

**23. What is the Memento pattern?**  
- Captures and restores an object’s state without violating encapsulation.  
- Useful for undo functionality.  
- Separates the concerns of saving state and managing state restoration.  
- Used in a text editor application for undo/redo features. Example:  

```csharp
public class Memento { public string State { get; } }
public class Originator
{
    private string state;
    public void SetState(string state) { this.state = state; }
    public Memento SaveState() => new Memento(state);
}
```

---

**24. What is the Command pattern?**  
- Encapsulates a request as an object, enabling parameterization and queuing.  
- Useful for undoable operations and logging changes.  
- Decouples sender and receiver of requests.  
- Used to implement an undo system in a task management app. Example:  

```csharp
public interface ICommand { void Execute(); void Undo(); }
public class CreateTaskCommand : ICommand
{
    public void Execute() { Console.WriteLine("Task Created"); }
    public void Undo() { Console.WriteLine("Task Creation Undone"); }
}
```

---

**25. What is Event Sourcing?**  
- Captures all changes to an application state as a sequence of events.  
- Ensures immutability and traceability of data changes.  
- Used for audit logs and temporal queries.  
- Applied in an inventory system to track stock changes. Example:  

```csharp
public class Event { public string EventType; public DateTime Timestamp; }
public class EventStore { private List<Event> events = new(); public void AddEvent(Event e) => events.Add(e); }
```

---

**26. What are the benefits of CQRS?**  
- Separates command (write) and query (read) responsibilities for better scalability.  
- Optimizes performance by tailoring read and write models.  
- Improves maintainability by decoupling concerns.  
- Implemented for high-traffic e-commerce sites to scale queries independently.  

---

**27. What are the drawbacks of the Active Record pattern?**  
- Tight coupling between database and domain logic.  
- Poor testability due to direct database dependency.  
- Difficult to manage complex business logic in Active Records.  
- Faced challenges with Active Record in a legacy project, moving to Repository solved them.  

---

**28. What is the Command and Query Responsibility Segregation (CQRS) pattern?**  
- Splits write operations (commands) from read operations (queries).  
- Enables scaling reads and writes independently.  
- Improves performance and simplifies query optimization.  
- Used CQRS in an analytics app to handle large-scale reporting.  

---

**29. What are the advantages of using Dependency Injection?**  
- Promotes loose coupling and improves maintainability.  
- Makes unit testing easier by enabling mocking.  
- Enhances flexibility and reusability of components.  
- Injected services in my .NET API project for streamlined testing and modularity.  

---

**30. What are some reasons to use the Repository pattern?**  
- Centralizes data access logic and promotes code reuse.  
- Decouples business logic from database operations.  
- Simplifies testing by mocking repositories.  
- Used in conjunction with Unit of Work for transaction management.  

**31. What is an Aggregate Root in the context of the Repository pattern?**  
- It is the primary entity that controls the lifecycle of a group of related objects.  
- Ensures that all changes to related objects go through the root entity.  
- Maintains consistency and prevents direct access to related objects.  
- Used Aggregate Roots in an e-commerce project for managing orders and their line items. Example:  

```csharp
public class Order
{
    public int Id { get; set; }
    public List<OrderItem> Items { get; } = new();
    public void AddItem(OrderItem item) => Items.Add(item);
}
```

---

**32. In OOP, what is the difference between the Repository pattern and a Service Layer?**  
- The Repository pattern handles data access and persistence logic.  
- The Service Layer contains business logic and coordinates operations across repositories.  
- Repositories focus on CRUD operations, while services orchestrate workflows.  
- Used Service Layer in conjunction with Repository to encapsulate business rules. Example:  

```csharp
public class OrderService
{
    private readonly IRepository<Order> _repository;
    public OrderService(IRepository<Order> repository) { _repository = repository; }
    public void PlaceOrder(Order order) { /* Business logic */ _repository.Add(order); }
}
```

---

**33. Is Unit of Work equal to Transaction or is it more than that?**  
- Unit of Work coordinates changes across multiple repositories in a single transaction.  
- Transactions are low-level, while Unit of Work is higher-level and manages multiple operations.  
- Unit of Work also tracks changes to entities to minimize database interactions.  
- Used Unit of Work in a multi-repository scenario to commit changes atomically. Example:  

```csharp
public class UnitOfWork : IUnitOfWork
{
    private readonly DbContext _context;
    public UnitOfWork(DbContext context) { _context = context; }
    public void Commit() { _context.SaveChanges(); }
}
```

---

**34. When should I use the Active Record vs. Repository pattern?**  
- Use Active Record for simpler applications where domain logic is minimal.  
- Use Repository for complex systems with intricate business rules and large teams.  
- Repository promotes separation of concerns, making it more testable.  
- Transitioned from Active Record to Repository in a project to better manage complexity.  

---

**35. What is the Interpreter pattern?**  
- Defines a grammar for a language and an interpreter to interpret sentences in the language.  
- Useful for parsing and evaluating expressions.  
- Promotes extensibility by allowing new grammar rules.  
- Used this pattern to evaluate mathematical expressions in a custom scripting language. Example:  

```csharp
public interface IExpression { int Interpret(); }
public class Number : IExpression
{
    private readonly int _number;
    public Number(int number) { _number = number; }
    public int Interpret() => _number;
}
```

---

**36. What is the Abstract Factory pattern?**  
- Provides an interface for creating families of related objects without specifying their concrete classes.  
- Useful for creating platform-specific implementations.  
- Promotes consistency across products in the same family.  
- Used for generating UI components for different operating systems. Example:  

```csharp
public interface IUIFactory { IButton CreateButton(); }
public class WindowsUIFactory : IUIFactory { public IButton CreateButton() => new WindowsButton(); }
```

---

**37. What is the Adapter pattern?**  
- Converts the interface of a class into another interface the client expects.  
- Promotes compatibility between incompatible interfaces.  
- Used for integrating third-party libraries in legacy systems.  
- Applied this pattern to use a new logging framework in an existing application. Example:  

```csharp
public interface ILogger { void Log(string message); }
public class LogAdapter : ILogger
{
    private readonly ThirdPartyLogger _logger;
    public LogAdapter(ThirdPartyLogger logger) { _logger = logger; }
    public void Log(string message) => _logger.WriteLog(message);
}
```

---

**38. What is the Bridge pattern?**  
- Decouples abstraction from implementation so that they can vary independently.  
- Useful for designing cross-platform systems.  
- Promotes flexibility and scalability in design.  
- Used for implementing shape rendering in a graphics application. Example:  

```csharp
public interface IRenderer { void Render(string shape); }
public class Circle
{
    private readonly IRenderer _renderer;
    public Circle(IRenderer renderer) { _renderer = renderer; }
    public void Draw() => _renderer.Render("Circle");
}
```

---

**39. What does "program to interfaces, not implementations" mean?**  
- Encourages using abstractions (interfaces) instead of concrete classes.  
- Promotes flexibility, making code more extensible and testable.  
- Reduces coupling between modules and facilitates dependency injection.  
- Followed this principle to inject dependencies in a modular application. Example:  

```csharp
public interface INotification { void Send(string message); }
```

---

**40. What is the Decorator pattern?**  
- Dynamically adds new behaviors to objects without altering their structure.  
- Promotes code reuse and adherence to the open/closed principle.  
- Used this pattern to add logging and validation to services. Example:  

```csharp
public interface INotifier { void Notify(string message); }
public class EmailNotifier : INotifier { public void Notify(string message) { /* Email sending */ } }
public class LoggingNotifier : INotifier
{
    private readonly INotifier _notifier;
    public LoggingNotifier(INotifier notifier) { _notifier = notifier; }
    public void Notify(string message)
    {
        Console.WriteLine("Logging: " + message);
        _notifier.Notify(message);
    }
}
```

---

**41. What is the Prototype pattern?**  
- Creates new objects by copying an existing object.  
- Useful for creating objects with similar configurations.  
- Promotes efficiency when object creation is expensive.  
- Used this pattern for cloning configurations in a template-based system. Example:  

```csharp
public class Prototype : ICloneable
{
    public string Name { get; set; }
    public object Clone() => MemberwiseClone();
}
```

---

**42. What is the Facade pattern?**  
- Provides a simplified interface to a complex subsystem.  
- Reduces the dependency of client code on subsystem classes.  
- Used this pattern to simplify access to third-party APIs in a project. Example:  

```csharp
public class EmailService
{
    public void SendEmail(string to, string subject, string body) { /* Implementation */ }
}
public class NotificationFacade
{
    private readonly EmailService _emailService = new();
    public void Notify(string message) => _emailService.SendEmail("user@example.com", "Notification", message);
}
```

---

**43. What is the difference between Proxy and Decorator patterns?**  
- Proxy controls access to the object, while Decorator adds new behavior.  
- Proxy focuses on resource management; Decorator enhances functionality.  
- Both follow similar structures but serve different purposes.  
- Used Proxy for caching and Decorator for dynamic feature extension in different projects.  

---

**44. What are the differences between a Static class and a Singleton class?**  
- A Static class cannot be instantiated; a Singleton ensures a single instance.  
- Singleton allows controlled initialization; Static does not manage state.  
- Singleton enables lazy loading and dependency injection.  
- Used Singleton for shared configurations and Static for utility methods.  

---

**45. When should I use the Composite design pattern?**  
- Use when you need to treat individual objects and compositions uniformly.  
- Ideal for hierarchical structures like file systems or menus.  
- Simplifies client code by providing a unified interface.  
- Implemented for rendering nested UI elements in a web application. Example:  

```csharp
public interface IComponent { void Render(); }
public class Composite : IComponent
{
    private List<IComponent> _children = new();
    public void Add(IComponent component) => _children.Add(component);
    public void Render() { foreach (var child in _children) child.Render(); }
}
```  

**46. What is the Observer pattern?**  
- Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified.  
- Useful for implementing publish-subscribe mechanisms.  
- Promotes loose coupling between subjects and observers.  
- Used this pattern to notify multiple components of state changes in an Angular project. Example:  

```csharp
public class Subject
{
    private readonly List<IObserver> observers = new();
    public void Attach(IObserver observer) => observers.Add(observer);
    public void Notify() { foreach (var observer in observers) observer.Update(); }
}
public interface IObserver { void Update(); }
```

---

**47. What is the Mediator pattern?**  
- Encapsulates interactions between multiple objects, promoting loose coupling.  
- Centralizes communication to simplify object dependencies.  
- Useful for managing complex workflows with multiple interacting components.  
- Used this pattern in a chat application to coordinate user interactions. Example:  

```csharp
public class ChatRoom
{
    public void ShowMessage(string user, string message) => Console.WriteLine($"{user}: {message}");
}
```

---

**48. How is the Bridge pattern different from the Adapter pattern?**  
- Bridge separates abstraction and implementation, allowing them to vary independently.  
- Adapter makes an existing class compatible with a new interface.  
- Bridge is used proactively for extensibility, while Adapter solves compatibility issues retroactively.  
- Applied Bridge for modular development and Adapter for legacy integration.  

---

**49. What is the Service Locator pattern?**  
- Provides a central registry for locating services in an application.  
- Decouples client code from dependency initialization.  
- Can make code harder to trace compared to Dependency Injection.  
- Used this pattern in legacy codebases where DI was not feasible. Example:  

```csharp
public class ServiceLocator
{
    private static readonly Dictionary<Type, object> Services = new();
    public static void Register<T>(T service) => Services[typeof(T)] = service;
    public static T Resolve<T>() => (T)Services[typeof(T)];
}
```

---

**50. What is the Flyweight pattern?**  
- Reduces memory usage by sharing common parts of objects that are expensive to instantiate.  
- Useful when dealing with large numbers of objects with shared state.  
- Separates intrinsic (shared) and extrinsic (unique) data.  
- Used this pattern for rendering thousands of text characters in a graphics application. Example:  

```csharp
public class Flyweight
{
    private readonly string _intrinsicState;
    public Flyweight(string intrinsicState) { _intrinsicState = intrinsicState; }
    public void Operation(string extrinsicState) => Console.WriteLine($"{_intrinsicState} - {extrinsicState}");
}
```

---

**51. What is the difference between Strategy and State design patterns?**  
- Strategy allows choosing an algorithm at runtime, while State changes behavior based on object state.  
- Strategy focuses on behavior delegation; State focuses on transitions between states.  
- Both promote flexibility but serve different purposes.  
- Used Strategy for dynamic sorting and State for a finite state machine in different projects.  

---

**52. What are some disadvantages of Dependency Injection?**  
- Can make code harder to read and debug due to indirection.  
- Requires additional setup and configuration, increasing complexity.  
- Overuse can lead to an explosion of interfaces and abstractions.  
- Faced challenges with overly complex DI in a large-scale .NET application.  

---

**53. What is the relationship between Repository and Unit of Work?**  
- Repository manages CRUD operations for entities.  
- Unit of Work coordinates transactions across multiple repositories.  
- Together, they ensure consistency and reduce database interaction.  
- Implemented this combination to handle operations on multiple aggregates atomically.  

---

**54. Why would I use the Chain of Responsibility over a Decorator?**  
- Chain of Responsibility processes requests in a sequence, allowing multiple handlers.  
- Decorator adds behavior dynamically to a single object.  
- Use Chain for request processing workflows; use Decorator for extensible functionality.  
- Applied Chain in a middleware pipeline and Decorator for feature toggles in projects.  

---

**55. Why shouldn't I use the Repository pattern with Entity Framework?**  
- EF already provides a DbContext, which acts as a repository.  
- Adding another Repository layer can lead to redundant abstractions.  
- Complex repositories may hide EF features like LINQ and tracking.  
- Used EF directly in simple projects but added Repository for complex systems with business logic.  

---

**56. When would you use the Builder pattern? Why not just use the Factory pattern?**  
- Use Builder for constructing complex objects step-by-step.  
- Factory is suitable for creating objects without complex configuration.  
- Builder separates the construction process from the representation.  
- Used Builder for configuring multi-step object creation in a reporting tool. Example:  

```csharp
public class ReportBuilder
{
    private Report _report = new();
    public ReportBuilder AddTitle(string title) { _report.Title = title; return this; }
    public Report Build() => _report;
}
```

---

**57. What is the difference between Composition and Inheritance?**  
- Composition involves "has-a" relationships, while Inheritance represents "is-a" relationships.  
- Composition is more flexible and avoids tight coupling.  
- Inheritance can lead to brittle hierarchies if overused.  
- Used Composition for dynamic behavior and Inheritance for shared attributes in a UI library.  

---

**58. How should I group my Repositories when using the Repository pattern?**  
- Group repositories by aggregate roots or domain areas for better modularity.  
- Avoid creating a repository for every entity; focus on aggregates.  
- Centralize common logic in a base repository when possible.  
- Organized repositories by domain in an e-commerce system: `OrderRepository`, `ProductRepository`, etc.  

---

**59. Is the Repository pattern the same as the Active Record pattern?**  
- Repository separates domain logic from database access, while Active Record combines them.  
- Repository promotes testability and decoupling.  
- Active Record is simpler for smaller projects but harder to scale for complex systems.  
- Migrated from Active Record to Repository in a project to simplify testing.  

---

**60. What would you choose: a Repository pattern or "smart" business objects?**  
- Repository pattern for clear separation of data access and domain logic.  
- Smart business objects for simpler, self-contained applications.  
- Repository scales better for large systems, while smart objects are quick for prototypes.  
- Chose Repository for an enterprise app requiring complex query handling.  

**61. Could you explain some benefits of the Repository pattern?**  
- Simplifies data access logic by providing a clean abstraction layer.  
- Promotes testability by allowing mock implementations.  
- Centralizes database access, reducing duplication across codebases.  
- Implemented this pattern to streamline data access in a multi-layered web application.  

---

**62. Could you explain the difference between Facade and Mediator patterns?**  
- Facade simplifies access to a complex subsystem by providing a unified interface.  
- Mediator manages communication between multiple objects without them knowing about each other.  
- Facade is about reducing system complexity; Mediator focuses on object interaction.  
- Used Facade for API calls and Mediator for event-driven workflows in projects.  

---

**63. What is the difference between Template and Strategy patterns?**  
- Template defines the skeleton of an algorithm, deferring steps to subclasses.  
- Strategy defines a family of algorithms and allows them to be interchangeable.  
- Template enforces structure; Strategy promotes flexibility.  
- Used Template for defining report generation steps and Strategy for dynamic payment methods.  

---

**64. What is the Deadly Diamond of Death in design patterns?**  
- Refers to ambiguity in multiple inheritance when a class inherits from two classes with a common ancestor.  
- Common in languages that support multiple inheritance (e.g., C++).  
- Avoided in languages like C# or Java by using interfaces or composition.  
- Resolved this issue in a C++ project by ensuring proper virtual inheritance.  

---

**65. Could you explain the differences between Facade, Proxy, Adapter, and Decorator design patterns?**  
- **Facade**: Simplifies access to a subsystem by providing a single interface.  
- **Proxy**: Controls access to an object (e.g., caching, logging).  
- **Adapter**: Converts an interface into another compatible interface.  
- **Decorator**: Dynamically adds behavior to an object without altering its structure.  
- Applied these patterns in different scenarios: Facade for API, Proxy for caching, Adapter for legacy systems, and Decorator for runtime extensions.  

---

**66. Can we use CQRS without Event Sourcing?**  
- Yes, CQRS can be implemented without Event Sourcing.  
- Event Sourcing is optional and records changes as events; CQRS separates reads and writes.  
- Often used together but not inherently dependent on each other.  
- Implemented CQRS with traditional database reads in a reporting tool without Event Sourcing.  

---

**67. What's the difference between Dependency Injection and Service Locator patterns?**  
- Dependency Injection provides dependencies explicitly, while Service Locator allows components to fetch them.  
- DI promotes explicit dependencies and is more transparent.  
- Service Locator can lead to hidden dependencies and harder-to-trace code.  
- Switched from Service Locator to DI in a .NET Core project for better testability.  

---

**68. How should I add an object into a collection maintained by an Aggregate Root?**  
- Use a method on the Aggregate Root to encapsulate the operation.  
- This ensures business rules are enforced during object addition.  
- Direct manipulation of collections violates the Aggregate's consistency boundary.  
- Example from an e-commerce project:  

```csharp
public class Order
{
    private readonly List<OrderItem> _items = new();
    public void AddItem(OrderItem item) => _items.Add(item); // Enforce rules here
}
```

---

**69. What is the Data Mapper pattern?**  
- Maps data between in-memory objects and a database while keeping them independent.  
- Promotes decoupling between domain logic and database schemas.  
- Used by tools like Entity Framework and Hibernate.  
- Example:  

```csharp
public class DataMapper
{
    public Order MapToOrder(DataRow row) => new Order { Id = (int)row["Id"], Name = (string)row["Name"] };
}
```

---

**70. What is the Repository and Specification pattern combination?**  
- Specification defines criteria for querying data, and Repository implements data access.  
- This combination simplifies complex queries and keeps them reusable.  
- Used to filter orders dynamically in a .NET application. Example:  

```csharp
public class OrderSpecification
{
    public Expression<Func<Order, bool>> Criteria { get; } = order => order.IsPaid;
}
```

---

**71. What is a Domain Event in DDD?**  
- Represents something that happened in the domain that is significant to business.  
- Often used to trigger side effects or notify other parts of the system.  
- Encapsulates changes to the state in an immutable event object.  
- Example:  

```csharp
public class OrderPlacedEvent
{
    public int OrderId { get; }
    public OrderPlacedEvent(int orderId) { OrderId = orderId; }
}
```

---

**72. What is the Repository pattern in CQRS?**  
- Provides separate repositories for queries and commands.  
- Query repositories focus on read operations, and command repositories focus on writes.  
- Promotes clarity and scalability in CQRS implementations.  
- Example structure: `OrderQueryRepository`, `OrderCommandRepository`.  

---

**73. What is an Anti-Corruption Layer (ACL)?**  
- Translates between different models or systems to maintain domain integrity.  
- Prevents external systems from polluting the internal domain model.  
- Used to integrate a legacy billing system with a modern payment service.  
- Example:  

```csharp
public class BillingAcl
{
    public ModernBillingRequest ConvertToModernRequest(LegacyBillingData legacyData) { /* Mapping logic */ }
}
```

---

**74. What is the purpose of a Value Object in DDD?**  
- Represents an immutable type defined by its attributes, not identity.  
- Promotes consistency and encapsulates logic related to attributes.  
- Used for reusable concepts like money, address, or date range.  
- Example:  

```csharp
public class Money
{
    public decimal Amount { get; }
    public string Currency { get; }
    public Money(decimal amount, string currency) { Amount = amount; Currency = currency; }
}
```

---

**75. What is a bounded context in Domain-Driven Design?**  
- Represents a logical boundary within which a domain model is consistent.  
- Defines clear separations of concerns between subdomains.  
- Reduces complexity by isolating models and logic.  
- Used bounded contexts to structure a microservices-based application.  