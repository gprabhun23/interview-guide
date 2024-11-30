1. **Difference between .NET Framework and .NET Core**  
.NET Framework is Windows-only, while .NET Core is cross-platform, supporting Windows, macOS, and Linux.  
.NET Framework is monolithic, while .NET Core is modular and lightweight.  
.NET Core offers better performance and supports modern development like microservices and containerization.  
.NET Core is open-source and community-driven, while .NET Framework is closed-source.  
I migrated a large .NET Framework project to .NET Core for containerization using Docker to deploy on Linux.  

2. **Garbage Collection in .NET and its Optimization in .NET Core**  
Garbage collection (GC) manages memory by automatically reclaiming unused objects to prevent memory leaks.  
GC works in generations (0, 1, 2) to optimize performance by focusing on short-lived objects.  
In .NET Core, GC is further optimized with server and workstation modes for multi-threaded environments.  
GC in .NET Core also includes enhancements for high-throughput applications, such as background garbage collection.  
I optimized memory usage in a high-load web API project by configuring server GC mode in .NET Core.  

3. **Dispose vs. Finalize in .NET**  
Dispose is a method for releasing unmanaged resources explicitly, used in conjunction with the IDisposable interface.  
Finalize is a method called by the garbage collector to clean up unmanaged resources when an object is no longer in use.  
Dispose is deterministic, giving developers control, while Finalize is non-deterministic and depends on garbage collection.  
Using Dispose with `using` ensures immediate resource cleanup, while Finalize introduces overhead and delayed cleanup.  
I implemented Dispose in a database connection manager to release resources promptly after each operation.  

4. **Asynchronous Programming in C#**  
Asynchronous programming enables non-blocking operations, improving responsiveness in applications.  
It uses async and await keywords to make asynchronous calls easier to write and read.  
Tasks represent ongoing operations and are central to asynchronous programming.  
Async methods return a Task or Task<T>, making it easier to chain operations.  
I used async/await in a file processing application to process multiple files without blocking the UI thread.  

5. **Task, async, and await in C#**  
Task represents an operation that may complete in the future, similar to a promise in JavaScript.  
Async modifies a method to indicate it can perform asynchronous operations.  
Await pauses the execution of an async method until the awaited Task completes.  
They work together to make asynchronous code readable and maintainable, avoiding callbacks.  
I used Task.Run and await to offload CPU-intensive image processing in a web application.  

6. **Value Types vs. Reference Types in C#**  
Value types store data directly in the stack, while reference types store a reference to data in the heap.  
Value types include primitives like int and structs, while reference types include classes and objects.  
Changes to value types do not affect the original variable, while changes to reference types do.  
Boxing and unboxing allow converting between value and reference types.  
I used value types for lightweight data like coordinates and reference types for complex objects like database models.  

7. **Exception Handling in C# (try, catch, finally)**  
Try defines a block of code where exceptions might occur.  
Catch handles exceptions, allowing custom error handling.  
Finally executes code regardless of whether an exception was thrown, typically for cleanup.  
Exception handling ensures robustness and prevents crashes due to unhandled errors.  
I used try-catch-finally in a file upload service to handle IO exceptions and ensure resource cleanup.  

8. **Const, Readonly, and Static in C#**  
Const values are compile-time constants and cannot be changed after compilation.  
Readonly values are runtime constants and can only be assigned once, either inline or in the constructor.  
Static members belong to the class rather than an instance, allowing shared data or methods.  
Const values cannot have runtime dependencies, while readonly values can.  
I used readonly for configuration properties that depended on runtime input, such as environment variables.  

9. **Dependency Injection in .NET Core**  
Dependency injection (DI) is a design pattern that provides dependencies rather than creating them manually.  
It improves testability, maintainability, and decoupling of components.  
.NET Core has built-in support for DI through IServiceCollection and IServiceProvider.  
The three DI registrations in .NET Core are transient, scoped, and singleton.  
I implemented DI in an API project to inject logging and database services, improving testability and modularity.  

10. **Delegates in C#**  
Delegates are type-safe function pointers used to encapsulate methods.  
They can point to static or instance methods and allow methods to be passed as parameters.  
Single-cast delegates refer to one method, while multicast delegates refer to multiple methods.  
Events use delegates to provide a publish-subscribe mechanism for signaling.  
I used delegates in a real-time notification system to dynamically invoke appropriate handlers.  

11. **LINQ in .NET**  
LINQ (Language Integrated Query) enables querying data using C# syntax for collections, databases, and XML.  
It provides methods like Select, Where, and Join for concise and readable queries.  
LINQ supports deferred execution, meaning queries are executed only when enumerated.  
LINQ integrates seamlessly with databases via LINQ to SQL and Entity Framework.  
I used LINQ to filter and group large datasets in a report-generation feature for a financial system.  

12. **Attributes in C#**  
Attributes provide metadata about classes, methods, or properties at runtime.  
They are applied using square brackets and can influence behavior or processing.  
Custom attributes are defined by inheriting from the Attribute base class.  
Attributes are useful for serialization, validation, and runtime inspection.  
I created a custom attribute to enforce validation rules on API inputs in a web application.  

13. **Partial Classes in C#**  
Partial classes allow splitting a single class across multiple files.  
They improve code organization and make large classes more maintainable.  
All parts of a partial class are combined into one at compile time.  
Partial classes are commonly used in auto-generated code like designer files.  
I used partial classes in a WPF project to separate auto-generated and manual code for a UI component.  

14. **Extension Methods in C#**  
Extension methods add new functionality to existing types without modifying them.  
They are defined as static methods in a static class and use the `this` keyword for the extended type.  
Extension methods improve code readability and reusability.  
They cannot override existing methods and are invoked like instance methods.  
I created an extension method for IEnumerable to calculate the median in a data analysis project.  

15. **Readonly vs. Const in C#**  
Readonly values are runtime constants, while const values are compile-time constants.  
Readonly values can be assigned in the constructor, while const must be assigned at declaration.  
Readonly supports reference types, while const is restricted to primitive types and strings.  
Readonly allows different values for instances, while const is shared across all instances.  
I used readonly for API base URLs that depended on runtime configurations in a multi-environment project.  

16. **Boxing and Unboxing in C#**  
Boxing converts a value type to a reference type by wrapping it in an object.  
Unboxing extracts the value type from the boxed object.  
Boxing and unboxing involve performance overhead due to heap allocation and type conversion.  
Avoid excessive boxing and unboxing to maintain performance in high-frequency operations.  
I optimized a project by replacing boxed value types in a logging system with generic methods to reduce GC pressure.  

17. **Significance of IEnumerable and IQueryable in C#**  
IEnumerable is used for in-memory, forward-only iteration of collections.  
IQueryable extends IEnumerable for querying data sources like databases with deferred execution.  
IEnumerable processes all data in memory, while IQueryable translates queries into database commands.  
IEnumerable is suitable for small datasets, while IQueryable is preferred for large datasets in remote sources.  
I used IQueryable in an Entity Framework project to optimize database queries and reduce memory usage.  

18. **Difference Between ICollection, IList, and IEnumerable**  
ICollection provides size, addition, removal, and containment operations on collections.  
IList extends ICollection by supporting indexed access and item replacement.  
IEnumerable is read-only and supports forward-only iteration over collections.  
ICollection and IList are mutable, while IEnumerable is immutable and deferred-execution friendly.  
I used IList in a project to manage a dynamically sortable and filterable list of user accounts.  

19. **Difference Between ref and out Parameters in C#**  
ref requires variables to be initialized before passing them to the method.  
out does not require initialization, but the method must assign a value before returning.  
Both ref and out pass variables by reference, allowing modifications within methods.  
ref is used for modifying existing data, while out is used for returning multiple outputs.  
I used out parameters in a function to return status codes along with messages in a logging system.  

20. **Memory Management in .NET**  
.NET uses garbage collection (GC) to manage memory automatically by cleaning up unused objects.  
Managed memory is divided into generations (0, 1, 2) for efficient collection.  
Developers control memory indirectly by managing object lifetimes and using Dispose or `using` statements.  
Large object heaps (LOH) require special handling to minimize fragmentation and GC overhead.  
I optimized a memory-intensive application by analyzing GC logs and minimizing LOH allocations using pooled objects.  

21. **Nullable Types in C#**  
Nullable types allow value types to hold a null value using the `?` syntax (e.g., `int?`).  
They are useful for representing missing or undefined data, like database fields.  
Nullable types provide methods like HasValue and Value for null checks and access.  
They help reduce null reference exceptions and improve code clarity.  
I used nullable types in an API to handle optional query parameters for filtering user data.  

22. **Exception Handling Across Functions in C#**  
Exceptions propagate up the call stack until a matching catch block is found.  
Try-catch blocks should be used sparingly, ideally at high-level layers for centralized handling.  
Global exception handling can be implemented using middleware in .NET Core.  
Avoid catching general exceptions like `Exception` unless necessary.  
I implemented centralized exception logging in a middleware to track errors in a .NET Core API.  

23. **Purpose of Sealed Class in C#**  
A sealed class cannot be inherited, ensuring no modifications through derived classes.  
Sealed classes are useful for scenarios where behavior must remain consistent.  
They improve performance by allowing certain compiler optimizations.  
Sealed methods can also be defined in unsealed classes to prevent overriding.  
I used sealed classes in a project to secure core encryption logic against unintended changes.  

24. **Multithreading in C#**  
Multithreading enables concurrent execution of multiple threads for better performance.  
Threads can be created manually using the `Thread` class or managed using the Task Parallel Library (TPL).  
.NET provides synchronization constructs like locks, Mutex, and Monitor to manage shared resources.  
Parallel processing can be implemented using `Parallel.For` and PLINQ for scalable workloads.  
I implemented multithreading in a data processing tool to handle simultaneous file uploads and parsing.  

25. **Significance of async and await Keywords in C#**  
async enables methods to run asynchronously, improving responsiveness.  
await pauses execution until the awaited operation completes, avoiding thread blocking.  
They simplify asynchronous programming by eliminating callbacks.  
Only methods returning Task, Task<T>, or void can use async.  
I used async and await in a project to fetch API data concurrently without blocking the UI thread.  

26. **Difference Between Shallow Copy and Deep Copy in .NET**  
Shallow copy duplicates the object but retains references to nested objects.  
Deep copy creates a completely independent copy, including nested objects.  
Shallow copies are faster but may cause unintended modifications to shared data.  
Deep copies require manual cloning or serialization for complex structures.  
I implemented deep copying in a project to create independent backup configurations for user profiles.  

27. **Using `this` Keyword in Static Methods**  
Static methods belong to the class, not an instance, so they cannot access instance members.  
The `this` keyword refers to the current instance and is not available in static methods.  
Static methods can only operate on static fields or methods.  
Instance members can be accessed from static methods by passing the object explicitly.  
I avoided static methods when accessing instance data in a utility class to maintain clean design.  

28. **Exception Handling in Nested Function Calls**  
Exceptions propagate up the call stack until handled or crash the application.  
Each method in the hierarchy can have its own try-catch block.  
Alternatively, centralized error handling can catch exceptions at the top level.  
Logging exceptions at every layer helps trace error origins.  
I implemented centralized exception handling in a middleware to catch and log errors in nested function calls.  

29. **Difference Between Synchronous and Asynchronous Programming in .NET**  
Synchronous programming executes tasks sequentially, blocking the thread until completion.  
Asynchronous programming allows tasks to run concurrently without blocking the thread.  
Async improves performance for I/O-bound and long-running operations.  
Threads are freed up in async programming, making it more scalable.  
I used asynchronous programming in a REST API to handle high traffic efficiently by avoiding thread-blocking calls.  

30. **Custom Exceptions in C#**  
Custom exceptions inherit from the base Exception class.  
They allow defining meaningful error messages and custom properties for specific error scenarios.  
Always include descriptive error messages and optional inner exceptions for better debugging.  
Custom exceptions should follow naming conventions ending with "Exception".  
I created a custom `InvalidUserInputException` to handle validation errors in a form-processing API.  
31. **Generics in C#**  
Generics enable type safety and reusability by defining classes or methods with type parameters.  
They reduce runtime type errors by enforcing type constraints at compile time.  
Generics eliminate the need for boxing and unboxing, improving performance.  
Common generic types include `List<T>`, `Dictionary<TKey, TValue>`, and custom generic classes or methods.  
I used generics in a repository pattern to create a reusable data access layer for multiple entity types.  

32. **Yield Keyword in C#**  
The `yield` keyword simplifies iterator implementation by returning elements one at a time.  
It allows creating custom iterators without building intermediate collections.  
When a `yield return` is encountered, the current position is saved for the next iteration.  
The `yield break` statement ends the iteration immediately.  
I used `yield` in a file-processing application to stream large log files line by line, avoiding memory overhead.  

33. **Using Statement in .NET**  
The `using` statement ensures proper disposal of unmanaged resources by calling Dispose automatically.  
It is used with types implementing the `IDisposable` interface, like files, streams, and database connections.  
The `using` block provides a cleaner and safer way to manage resources.  
With C# 8, `using` declarations simplify scoping by omitting braces.  
I used `using` in a project to manage database connections, ensuring proper release even during exceptions.  

34. **Value Type vs. Reference Type in C#**  
Value types store data directly on the stack and include primitives like `int`, `bool`, and structs.  
Reference types store references to data in the heap and include classes, objects, and arrays.  
Value types are passed by value, while reference types are passed by reference.  
Changes to reference types affect the original object, unlike value types.  
I used value types for lightweight objects like coordinates and reference types for complex entities like users.  

35. **Abstract Class vs. Interface in C#**  
Abstract classes can have both implemented and abstract methods, while interfaces define only abstract methods (before C# 8).  
Classes can inherit only one abstract class but implement multiple interfaces.  
Abstract classes allow fields and constructors; interfaces do not.  
Interfaces are better for defining contracts, while abstract classes provide base functionality.  
I used an interface for defining payment gateways and an abstract class for shared gateway logic in an e-commerce project.  

36. **Writing Method Bodies in Interfaces**  
C# 8 introduced default interface methods, allowing method bodies in interfaces.  
Default methods provide implementation that can be overridden by implementing classes.  
They enable adding functionality without breaking existing implementations.  
Only interfaces with default implementations can include method bodies; fields are still not allowed.  
I added a default logging implementation in an interface to streamline logging in multiple services.  

37. **Preventing Inheritance in C#**  
Use the `sealed` keyword to prevent classes from being inherited.  
Mark methods as `sealed` in a derived class to prevent further overriding.  
Use private constructors in singleton classes to prevent inheritance or instantiation.  
A combination of internal access modifiers and sealed classes enhances security for internal APIs.  
I used a sealed class for encryption utilities to ensure consistency and avoid inheritance-related bugs.  

38. **Overloading vs. Overriding in C#**  
Overloading allows multiple methods with the same name but different signatures in the same class.  
Overriding allows a derived class to modify the behavior of a virtual or abstract method in the base class.  
Overloading is resolved at compile time, while overriding is resolved at runtime.  
Overriding requires the `override` keyword; overloading does not.  
I used overriding in a base controller to customize API error handling and overloading for flexible input methods.  

39. **Purpose of Access Modifiers in C#**  
Access modifiers control the visibility and accessibility of classes, methods, and fields.  
`public` makes members accessible everywhere, while `private` restricts access to the containing class.  
`protected` allows access in the same class and derived classes, while `internal` limits it to the same assembly.  
They ensure encapsulation, improving maintainability and security of code.  
I used `internal` in a library project to expose helper methods only within the assembly.  

40. **CLR Memory Management in .NET**  
The Common Language Runtime (CLR) manages memory through garbage collection.  
Memory is allocated in managed heaps: small object heaps (SOH) and large object heaps (LOH).  
Garbage collection runs in generations to optimize performance by focusing on short-lived objects.  
Developers can use `Dispose`, `using`, or finalizers for deterministic cleanup of unmanaged resources.  
I analyzed GC behavior in a high-load API project using performance monitoring tools to minimize memory fragmentation.  

41. **Just-In-Time (JIT) Compiler in C#**  
The JIT compiler translates Intermediate Language (IL) into machine code at runtime.  
It enables platform-specific optimizations for the executing environment.  
JIT includes different modes like Normal, Pre-JIT (via NGen), and Tiered JIT for performance tuning.  
Code is compiled only when needed, reducing startup time but potentially increasing runtime latency.  
I used ReadyToRun (R2R) in a .NET Core project to precompile code for faster startup in a containerized environment.  

42. **Managed vs. Unmanaged Code in C#**  
Managed code runs within the CLR, providing memory management, type safety, and security.  
Unmanaged code executes outside the CLR, typically written in C or C++ and accessed via interop.  
Managed code is garbage-collected, while unmanaged code requires manual memory management.  
Interop tools like P/Invoke and COM are used to bridge managed and unmanaged code.  
I integrated unmanaged C++ libraries in a .NET Core project using P/Invoke for advanced image processing.  

43. **Accessing Unmanaged Code from Managed Code**  
P/Invoke is used to call C-style unmanaged functions from managed code.  
COM interop allows managed code to interact with unmanaged COM objects.  
The `DllImport` attribute specifies the unmanaged library and entry point for interop.  
Memory management must be handled carefully to prevent leaks when working with unmanaged resources.  
I used P/Invoke to call native Win32 APIs for custom window management in a desktop application.  

44. **Difference Between Array and List in C#**  
Arrays have fixed size, while lists are dynamic and can grow or shrink.  
Lists provide additional methods like Add, Remove, and Find, making them more flexible.  
Arrays are faster for direct indexing due to their static size and structure.  
Lists are part of the `System.Collections.Generic` namespace, supporting generic types.  
I used a list to store and manage dynamic user input in a real-time survey application.  

45. **Retrieving Type Information at Runtime in C#**  
Use `typeof` to get the `Type` of a class at compile time.  
Use `GetType()` on an instance to retrieve its runtime type information.  
Reflection allows detailed inspection and manipulation of metadata at runtime.  
The `is` and `as` operators can help determine and cast types safely.  
I used reflection to dynamically load plugins in an extensible application framework.  

46. **ASP.NET MVC 4.7 Project Components**  
An ASP.NET MVC project typically includes folders like **Models**, **Views**, and **Controllers** for the MVC pattern.  
The **App_Start** folder contains configuration files such as RouteConfig and FilterConfig.  
Static content like images, CSS, and JavaScript files are stored in the **Content** and **Scripts** folders.  
The **Web.config** file manages application settings and configuration.  
I structured an MVC project with Models for database entities, Controllers for business logic, and Views for rendering the UI.  

47. **Static Files in .NET Core Projects**  
Static files like images, CSS, and JavaScript are stored in the **wwwroot** folder.  
Static files must be explicitly enabled in the `Startup` class using `UseStaticFiles()`.  
Custom folders can be added under `wwwroot` for better organization (e.g., **images**, **css**, **js**).  
Static files are served directly without invoking the middleware pipeline.  
I stored a custom font in the `wwwroot/fonts` folder and configured it for a web project using relative paths.  

48. **Partial Views in ASP.NET MVC 5 vs. .NET Core**  
In both, partial views are used to render reusable UI components within a view.  
Partial views are invoked using `Html.Partial()` or `Html.RenderPartial()` in MVC 5, and `PartialAsync()` in .NET Core.  
.NET Core introduced tag helpers, such as `<partial>`, to simplify partial view rendering.  
Dependency injection is easier in .NET Core partial views using the Razor Pages model.  
I used partial views in both frameworks to display shared navigation bars and footers across multiple pages.  

49. **Four Ways to Return Data from a Controller to a View in ASP.NET MVC**  
Use a **ViewBag** to pass dynamic data.  
Use a **ViewData** dictionary for loosely typed data.  
Use a strongly typed **Model** for structured data.  
Pass data through **TempData**, which persists across requests.  
I returned a `ProductViewModel` as a strongly typed model in a product catalog project for better type safety.  

50. **Action Filters in ASP.NET MVC**  
Action filters allow executing code before or after an action method runs.  
Filters are implemented by inheriting from attributes like `ActionFilterAttribute`.  
Common filters include Authorization, Action, Result, and Exception filters.  
Filters can be applied at the action, controller, or global level.  
I created a custom logging filter to log API request details in an audit trail system.  

51. **Saving a Username in a Session in ASP.NET MVC and .NET Core**  
In ASP.NET MVC, use `Session["Username"] = value` and retrieve it with `Session["Username"]`.  
In .NET Core, use the `ISession` interface and `HttpContext.Session.SetString`/`GetString`.  
Session must be configured in `Startup.cs` using `AddSession()` and `UseSession()`.  
Sessions store data in-memory by default but can use distributed storage in .NET Core.  
I stored user preferences in sessions for a multi-user dashboard project using distributed Redis cache.  

52. **Handling File Uploads in .NET Core Controllers**  
Use the `IFormFile` interface to handle uploaded files in .NET Core.  
Bind files to an action method using the `[FromForm]` attribute.  
Files can be saved using `FileStream` to a desired directory.  
Validation for size, type, and content is crucial for security.  
I implemented file uploads in a document management system, ensuring secure storage with MIME type checks.  

53. **Middleware in .NET Core**  
Middleware is a pipeline component that processes HTTP requests and responses.  
Custom middleware is created by implementing a `RequestDelegate` and using the `Use` method.  
Middleware executes in order of registration in the `Startup.Configure` method.  
It can modify requests, add headers, or handle authentication and logging.  
I built middleware to detect the keyword "Iran" in URLs and return a custom error response for restricted access.  

54. **Adding Output Caching to an API Action Method in .NET Core**  
Use the `ResponseCache` attribute to enable output caching for an API method.  
Configure duration, location, and vary parameters for caching behavior.  
Caching reduces server load and improves performance for frequently accessed endpoints.  
Use distributed caching providers like Redis for scalable caching solutions.  
I implemented caching in an API to store search results for 5 minutes, reducing repeated database queries.  

55. **RabbitMQ and Its Usage**  
RabbitMQ is a message broker for implementing asynchronous communication between systems.  
It supports message queuing, routing, and delivery confirmations.  
Messages are exchanged via producers, queues, and consumers using the AMQP protocol.  
RabbitMQ is used for decoupled architecture in microservices, event-driven systems, and job processing.  
I used RabbitMQ in a project to handle background email notifications asynchronously from the main application flow.  

56. **HTTP Action Verbs Used in API Methods**  
`GET` retrieves data from the server.  
`POST` creates new resources on the server.  
`PUT` updates an existing resource or creates one if it doesn't exist.  
`DELETE` removes a resource from the server.  
I used all these verbs in a RESTful API for managing user profiles in a social networking application.  

57. **JWT Tokens and Implementation**  
JWT (JSON Web Tokens) is used for secure, stateless authentication.  
It consists of three parts: Header, Payload, and Signature.  
JWT is implemented in .NET Core using libraries like `Microsoft.AspNetCore.Authentication.JwtBearer`.  
In Angular, JWT is stored in `localStorage` or `sessionStorage` and attached to API requests using interceptors.  
I used JWT in a project to authenticate users securely across multiple microservices with token expiration and refresh logic.  

58. **Versioning an API in .NET Core and ASP.NET MVC**  
Use route versioning, such as `api/v1/endpoint`, for explicit versioning.  
Query string parameters or headers can also indicate the API version.  
ASP.NET Core provides the `Microsoft.AspNetCore.Mvc.Versioning` package for version management.  
Deprecate older versions gracefully by documenting the changes.  
I implemented API versioning in a project to support legacy clients while transitioning to a newer API design.  

59. **Docker and Its Use in Deployment**  
Docker is a platform for containerizing applications with their dependencies for consistent deployment.  
Containers are lightweight and portable, running the same way on different environments.  
Dockerfiles define the build instructions for creating application images.  
It is widely used for microservices, CI/CD pipelines, and scaling distributed systems.  
I used Docker to containerize a .NET Core API, ensuring seamless deployment on AWS ECS.  

60. **Purpose of Span<T> and Memory<T> in C#**  
Span<T> and Memory<T> are types for working with contiguous memory efficiently.  
They minimize allocations by allowing slicing without copying data.  
Span<T> works with stack-allocated memory, while Memory<T> supports heap-based and async-friendly scenarios.  
They improve performance in high-frequency operations like parsing or serialization.  
I used Span<T> in a project for parsing large CSV files to avoid unnecessary memory overhead.  

61. **Task.Run and Its Usage in .NET Applications**  
Task.Run queues work to a thread pool for parallel execution.  
It should be used for CPU-bound operations rather than I/O-bound tasks.  
Task.Run avoids blocking the main thread, enhancing responsiveness in applications.  
It is not recommended for long-running tasks or server-side code that already runs in a managed thread pool.  
I used Task.Run in a project to offload data processing tasks in a desktop application while keeping the UI responsive.  

62. **Source Generators in .NET**  
Source generators produce additional code during compilation based on existing code.  
They improve developer productivity by automating repetitive code tasks.  
Common use cases include generating DTOs, mappings, or validation logic.  
Source generators integrate with the Roslyn compiler, enabling custom code-generation scenarios.  
I implemented a source generator to create boilerplate CRUD methods for entities, reducing manual coding.  

63. **Readonly Modifier vs. Const in C#**  
`readonly` is used for instance-level fields and can be assigned during runtime or in constructors.  
`const` is used for compile-time constants and must have a fixed value.  
`readonly` fields can have different values per instance, while `const` is shared across all instances.  
Use `readonly` for runtime constants and `const` for values that won’t change across builds.  
I used a readonly field for configuration values loaded during application startup, such as file paths.  

64. **Role of IL (Intermediate Language) in .NET Runtime**  
IL is a CPU-independent instruction set generated from C# code during compilation.  
The JIT compiler converts IL to platform-specific machine code at runtime.  
IL provides portability and flexibility, allowing .NET applications to run on different architectures.  
Tools like ILSpy or dotnet CLI can inspect IL for debugging or learning purposes.  
I analyzed the IL of a complex LINQ query to understand how deferred execution was implemented.  

65. **Value Types and Reference Types with Examples in C#**  
Value types (e.g., int, float, struct) store data directly on the stack.  
Reference types (e.g., class, array, object) store a reference to data on the heap.  
Value types are copied when passed, while reference types share the same data reference.  
Boxing converts value types to reference types; unboxing does the reverse.  
In a project, I used a struct for coordinates (value type) and a class for customers (reference type) to model data efficiently.  

66. **Advantages of Record Types in C#**  
Records provide immutable object support with concise syntax.  
They are reference types but offer value-based equality checks.  
`with` expressions enable copying records with modifications to specific properties.  
Positional records simplify constructors and property declarations.  
I used records to define entities in a CQRS architecture, ensuring immutability and reliable comparison logic.  

67. **Parallel Processing in .NET Using Parallel.ForEach and PLINQ**  
Parallel.ForEach processes items concurrently across threads.  
PLINQ extends LINQ for parallel execution of queries on collections.  
Both approaches utilize the Task Parallel Library (TPL) for workload distribution.  
They optimize performance for CPU-bound operations but require careful synchronization for shared resources.  
I used Parallel.ForEach in a project to process and compress thousands of image files simultaneously.  

68. **Memory Leaks in .NET Applications**  
Memory leaks occur when managed objects remain in memory due to unintentional references.  
Leaks can arise from event handlers, static fields, or long-lived collections holding unused objects.  
Tools like dotMemory, CLR Profiler, or Visual Studio diagnostics can detect leaks.  
Garbage collection mitigates leaks, but unmanaged resources require explicit cleanup via Dispose.  
In a project, I resolved a memory leak caused by forgotten event handler subscriptions in a real-time monitoring tool.  

69. **Await Using Syntax in Asynchronous Programming**  
The `await using` syntax ensures proper disposal of asynchronous resources implementing `IAsyncDisposable`.  
It simplifies resource management for objects used in async code, such as streams and database connections.  
`await using` ensures deterministic cleanup without blocking threads.  
The feature improves readability and reduces boilerplate code for async disposable patterns.  
I applied `await using` in a project to manage database connections in async methods using Entity Framework Core.  

70. **Sealed Class and Its Purpose in C#**  
A sealed class cannot be inherited, ensuring no derived classes alter its behavior.  
It is useful for security or final implementations like utility or helper classes.  
Sealing methods in derived classes prevents further overrides.  
Sealed classes can improve runtime performance by enabling certain optimizations.  
I used a sealed class for encryption utilities in a banking project to guarantee behavior integrity.  

71. **Multithreading in C#**  
Multithreading allows running multiple threads concurrently to utilize system resources efficiently.  
C# provides classes like `Thread`, `Task`, and `ThreadPool` for thread management.  
Synchronization primitives like `lock`, `Monitor`, and `Mutex` avoid race conditions in shared resources.  
Parallelism libraries like `Parallel.For` and `PLINQ` simplify multithreaded tasks.  
I implemented multithreading in a stock market simulator to handle real-time price updates across multiple streams.  

72. **Synchronous vs. Asynchronous Programming in .NET**  
Synchronous code blocks execution until tasks complete, causing potential delays.  
Asynchronous programming allows tasks to run independently, improving responsiveness.  
The `async` and `await` keywords simplify async programming in C#.  
Asynchronous methods do not block threads, making them ideal for I/O-bound operations.  
I converted a synchronous API to asynchronous in a project to handle high user loads without degrading performance.  

73. **Custom Exceptions in C#**  
Custom exceptions inherit from the `Exception` class and provide domain-specific error details.  
They can include additional properties or methods for better context.  
Use `throw` to raise and `catch` to handle custom exceptions.  
Always include meaningful messages and consider inner exceptions for debugging.  
I created a `DataValidationException` in a project to standardize validation error reporting in a REST API.  

74. **Boxing and Unboxing in C#**  
Boxing converts a value type to a reference type, wrapping it in an object.  
Unboxing extracts the value type from the object, requiring explicit casting.  
Boxing incurs a performance overhead due to heap allocation.  
Avoid frequent boxing/unboxing in performance-critical scenarios by using generics.  
In a project, I replaced boxed collections with generic collections to improve efficiency in data processing.  

75. **Difference Between Shallow Copy and Deep Copy in .NET**  
A shallow copy duplicates only the top-level object, sharing references for nested objects.  
A deep copy duplicates the entire object hierarchy, creating independent nested objects.  
Shallow copies can lead to unintended changes in nested objects due to shared references.  
Deep copies are created using serialization, custom copying, or libraries like AutoMapper.  
I implemented deep copy logic in a project to clone configuration objects safely without impacting the originals.  

76. **Can This Keyword Be Used in Static Methods? Why or Why Not?**  
The `this` keyword refers to the current instance of the class.  
Static methods belong to the class, not an instance, so they cannot use `this`.  
Static methods cannot access instance members directly; they require an instance of the class.  
Use instance methods when you need to work with `this` or instance-specific data.  
I encountered this when designing utility methods, ensuring they were static as they didn’t rely on any instance.  

77. **Handling Exceptions in Nested Function Calls (A Calls B, B Calls C)**  
Use `try-catch` blocks in the calling methods (A, B, C) where specific handling is needed.  
Rethrow exceptions using `throw` in intermediate methods if higher-level methods should handle them.  
Use a global exception handler for unhandled exceptions in critical applications.  
AggregateException is useful for combining multiple exceptions in parallel or nested tasks.  
In a payment system, I propagated exceptions from validation methods to the main controller for consolidated logging.  

78. **Synchronous vs. Asynchronous Programming in .NET**  
Synchronous programming processes tasks sequentially, one at a time.  
Asynchronous programming allows multiple tasks to run concurrently, improving responsiveness.  
`Task`, `async`, and `await` are key components of asynchronous programming in .NET.  
Asynchronous methods are ideal for I/O-bound operations, while synchronous methods work for CPU-bound tasks.  
In a web scraper, I replaced synchronous requests with asynchronous ones to fetch data from multiple URLs concurrently.  

79. **Generics in .NET for Code Reusability and Type Safety**  
Generics enable type-safe data structures and methods that work with any type.  
They eliminate the need for type casting, reducing runtime errors.  
Generics are implemented using classes, interfaces, methods, and delegates.  
They improve performance by avoiding boxing/unboxing for value types.  
I used generic repository patterns in a project for managing database operations without duplicating code for each entity.  

80. **Yield Keyword in C#**  
`yield` returns elements of a collection one at a time during iteration.  
It is used with `IEnumerable` or `IEnumerable<T>` to implement custom iterators.  
`yield return` provides deferred execution, evaluating items only when needed.  
`yield break` stops the iteration prematurely.  
I used `yield` to create a custom paginator for large data sets, reducing memory consumption by loading only required items.  

81. **Using Statement for Resource Management in .NET**  
The `using` statement ensures that unmanaged resources are disposed of properly.  
It is syntactic sugar for a `try-finally` block that calls `Dispose`.  
`using` works with objects implementing the `IDisposable` interface.  
The `await using` syntax in C# 8+ supports asynchronous resource cleanup.  
I implemented `using` for database connections in a .NET Core project to prevent connection leaks.  

82. **Abstract Class vs. Interface in C#**  
Abstract classes can have implementation, while interfaces cannot (pre-C# 8).  
Classes can inherit from only one abstract class but can implement multiple interfaces.  
Abstract classes support constructors, while interfaces do not.  
Interfaces define a contract, while abstract classes are partially implemented blueprints.  
I used an abstract base class for common logic in a project and interfaces to enforce implementation-specific details across modules.  

83. **Method Body in Interfaces in C#**  
C# 8+ allows default implementations in interfaces using the `default` keyword.  
Default methods enable extending interfaces without breaking existing implementations.  
Interfaces with method bodies remain less powerful than abstract classes for maintaining state.  
Use default methods cautiously to avoid complexity in understanding interface behavior.  
I added a default logging method in an interface to provide optional behavior in a logging framework.  

84. **Preventing Inheritance in C#**  
Mark the class as `sealed` to prevent it from being inherited.  
Use private or internal constructors to restrict object instantiation.  
Apply the `NotInheritable` keyword in VB.NET (equivalent to sealed in C#).  
Combine `internal` with `sealed` to restrict access to specific assemblies.  
In a security library, I sealed classes for sensitive operations to ensure no tampering via inheritance.  

85. **Overloading vs. Overriding in Object-Oriented Programming**  
Overloading defines multiple methods with the same name but different parameters in the same class.  
Overriding changes the behavior of a base class method in a derived class using `virtual` and `override`.  
Overloading is compile-time polymorphism, while overriding is runtime polymorphism.  
Overloaded methods belong to the same class; overridden methods span base and derived classes.  
In a reporting system, I overloaded methods for different input types and overridden methods for custom report generation.  

86. **Access Modifiers in C#: Public, Private, Internal**  
`public` allows access from any code in the solution.  
`private` restricts access to the containing class only.  
`internal` restricts access to the same assembly.  
Access modifiers help encapsulate logic and expose only necessary functionality.  
In a library, I used internal for helper classes to ensure they were not exposed to external consumers.  

87. **Memory Management in .NET by CLR**  
The Common Language Runtime (CLR) manages memory through garbage collection (GC).  
GC identifies unused objects and reclaims their memory.  
Generational GC optimizes performance by dividing objects into generations.  
Developers must manually release unmanaged resources using Dispose or `using`.  
I resolved memory issues in a project by profiling GC activity and optimizing object lifetimes.  

88. **Just-In-Time (JIT) Compiler in .NET**  
The JIT compiler converts IL to machine code at runtime.  
It compiles code on a per-method basis, improving startup performance.  
JIT optimizations include inlining, loop unrolling, and dead code elimination.  
The AOT (Ahead of Time) compiler can complement JIT in .NET Core for faster startup.  
I monitored JIT performance in a financial app to ensure critical methods were optimized during runtime.  

89. **Managed vs. Unmanaged Code in C#**  
Managed code runs under the control of the CLR, which handles memory, exceptions, and security.  
Unmanaged code is executed directly by the OS, bypassing CLR services.  
C# primarily produces managed code but can interact with unmanaged libraries via P/Invoke.  
Memory leaks are less frequent in managed code but common in unmanaged code without proper cleanup.  
I integrated a C++ library with C# using unmanaged interop for a high-performance image processing module.  

90. **Accessing Unmanaged Code in C#**  
Use Platform Invocation (P/Invoke) to call unmanaged functions in native DLLs.  
The `DllImport` attribute specifies the DLL and entry point for the method.  
Marshalling handles data type conversions between managed and unmanaged environments.  
Release unmanaged resources explicitly using methods like `FreeLibrary`.  
I used P/Invoke in a project to access legacy hardware APIs, ensuring seamless integration with modern .NET applications.  