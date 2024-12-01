1. **What is Entity Framework, and how does it simplify data access?**  
- Entity Framework (EF) is an Object-Relational Mapping (ORM) framework for .NET, simplifying database access.  
- It enables developers to interact with databases using strongly typed objects without writing raw SQL.  
- EF handles tasks like data mapping, change tracking, and relationship management automatically.  
- By abstracting the database layer, EF allows developers to focus on business logic.  
- Example: In a project, EF was used to simplify CRUD operations by mapping database tables to C# classes, reducing boilerplate code.  

2. **Compare Entity Framework and Entity Framework Core.**  
- Entity Framework is a full-featured, Windows-specific ORM, while EF Core is cross-platform and lightweight.  
- EF Core offers better performance and support for new features like global query filters and shadow properties.  
- EF supports Database-First and Model-First approaches, while EF Core emphasizes Code-First with improved flexibility.  
- EF Core lacks some EF features, such as EDMX-based models and lazy loading (in earlier versions).  
- Example: EF Core was used in a .NET Core project for its cross-platform support and better performance in handling LINQ queries.  

3. **What are the different approaches to using EF, such as Code-First, Database-First, and Model-First?**  
- Code-First: Define your database schema using C# classes, and EF generates the database.  
- Database-First: Reverse-engineer the database schema into C# models.  
- Model-First: Create a visual model, and EF generates the database schema and classes.  
- Each approach is suited for different project requirements and developer preferences.  
- Example: In a recent project, the Code-First approach was preferred for its flexibility and alignment with agile development.  

4. **How do you handle migrations in EF Core?**  
- Migrations are used to manage database schema changes while preserving existing data.  
- Use the `Add-Migration` and `Update-Database` commands in the Package Manager Console or CLI.  
- Migrations track changes to models and apply them incrementally to the database.  
- Customize migration scripts to handle complex scenarios like seed data or renaming columns.  
- Example: Implemented a migration to add a new table for storing user preferences using `dotnet ef migrations add AddUserPreferences`.  

```csharp
public class ApplicationDbContext : DbContext
{
    public DbSet<UserPreference> UserPreferences { get; set; }
}
```

5. **What is lazy loading, and how does it differ from eager loading in EF?**  
- Lazy loading defers loading related data until it's explicitly accessed.  
- Eager loading loads related data upfront using `Include()` in LINQ queries.  
- Explicit loading manually loads related data using `Load()` after the initial query.  
- Lazy loading minimizes initial data retrieval but may result in multiple database calls.  
- Example: Eager loading was used to optimize query performance in a reporting module:  

```csharp
var users = context.Users.Include(u => u.Orders).ToList();
```  

6. **How do you configure relationships between tables in EF Core?**  
- Define relationships using navigation properties in entity classes.  
- Use Fluent API for more control over configurations in the `OnModelCreating` method.  
- Specify cardinality using methods like `HasOne`, `HasMany`, or `WithMany`.  
- Apply constraints like foreign keys using `HasForeignKey`.  
- Example: Configured a one-to-many relationship between `Order` and `OrderItem` entities:  

```csharp
modelBuilder.Entity<Order>()
    .HasMany(o => o.OrderItems)
    .WithOne(oi => oi.Order)
    .HasForeignKey(oi => oi.OrderId);
```  

7. **How do you write a LINQ query in Entity Framework?**  
- LINQ queries can be written using query syntax or method syntax.  
- LINQ allows filtering, sorting, grouping, and projecting data.  
- EF Core translates LINQ queries to SQL for execution.  
- Queries support eager loading, lazy loading, and filtering for specific data.  
- Example: Fetching orders placed in the last week using LINQ:  

```csharp
var recentOrders = context.Orders
    .Where(o => o.OrderDate >= DateTime.Now.AddDays(-7))
    .ToList();
```  

8. **What are the common performance optimization techniques in EF Core?**  
- Use `AsNoTracking` for read-only queries to disable change tracking.  
- Leverage eager loading with `Include` to minimize database calls.  
- Use projection to retrieve only required fields.  
- Optimize queries with proper indexing and by avoiding N+1 query issues.  
- Example: Optimized a dashboard query using eager loading and projections:  

```csharp
var data = context.Users
    .Include(u => u.Orders)
    .Select(u => new { u.Name, OrderCount = u.Orders.Count })
    .ToList();
```  

9. **How do you execute raw SQL queries in EF Core?**  
- Use the `FromSqlRaw` or `FromSqlInterpolated` methods for executing raw SQL.  
- Combine raw SQL with LINQ for complex scenarios.  
- Ensure proper parameterization to prevent SQL injection.  
- Use raw SQL queries for operations unsupported by LINQ or for performance tuning.  
- Example: Executed a raw SQL query to retrieve active users:  

```csharp
var activeUsers = context.Users
    .FromSqlRaw("SELECT * FROM Users WHERE IsActive = 1")
    .ToList();
```  

10. **Explain how to use the Fluent API in EF Core.**  
- Fluent API provides a programmatic way to configure entity mappings.  
- Override `OnModelCreating` in `DbContext` to define configurations.  
- Use Fluent API for configurations like keys, constraints, and relationships.  
- It offers greater control than data annotations.  
- Example: Configured a composite key using Fluent API:  

```csharp
modelBuilder.Entity<OrderDetail>()
    .HasKey(od => new { od.OrderId, od.ProductId });
```  

11. **What is change tracking in EF Core, and how does it work?**  
- EF Core tracks changes to entity properties to update the database.  
- It uses a `DbContext` to maintain the state of entities (Added, Modified, Deleted).  
- Change tracking is automatic for entities retrieved from the database.  
- It enables efficient updates by sending only changed fields.  
- Example: Updated a user record, and EF Core automatically tracked the changes:  

```csharp
var user = context.Users.Find(1);
user.Name = "Updated Name";
context.SaveChanges();
```  

12. **How do you handle concurrency in EF Core?**  
- Concurrency is managed using concurrency tokens like `RowVersion`.  
- Add a property with `[ConcurrencyCheck]` or `IsRowVersion` for tracking.  
- Handle `DbUpdateConcurrencyException` for conflicts.  
- Merge or reject changes based on business rules.  
- Example: Added a `RowVersion` property for handling concurrency conflicts:  

```csharp
public byte[] RowVersion { get; set; }
```  

13. **Can you explain the role of repositories and unit of work patterns with EF Core?**  
- Repository pattern abstracts data access logic.  
- Unit of Work ensures transactional consistency across multiple repositories.  
- These patterns decouple business logic from EF Core-specific operations.  
- Simplifies testing and promotes cleaner architecture.  
- Example: Used a repository pattern to handle user operations in a service layer.  

```csharp
public interface IUserRepository
{
    User GetUserById(int id);
}
```  

14. **What is the purpose of AsNoTracking in EF Core? When should it be used?**  
- `AsNoTracking` disables change tracking for read-only queries.  
- It improves performance by reducing memory usage.  
- Ideal for scenarios where entities are not updated.  
- Avoid using `AsNoTracking` for entities involved in updates.  
- Example: Used `AsNoTracking` for fetching report data to improve performance:  

```csharp
var users = context.Users.AsNoTracking().ToList();
```  

15. **How do you implement migrations in Entity Framework Core?**  
- Create migrations using `Add-Migration` and apply them with `Update-Database`.  
- Customize migration files to handle specific requirements.  
- Use `dotnet ef` CLI for migrations in cross-platform projects.  
- Rollback changes using `Remove-Migration` or revert to a previous migration.  
- Example: Created a migration to add an `IsActive` column to the `Users` table:  

```bash
dotnet ef migrations add AddIsActiveColumn
```  
16. **Explain the use of LINQ in EF Core.**  
- LINQ (Language Integrated Query) in EF Core allows querying databases using strongly typed C# code.  
- It supports operations like filtering, projection, grouping, and ordering using query or method syntax.  
- EF Core translates LINQ queries into SQL queries executed on the database server.  
- Example: A LINQ query to fetch active users and their roles:  

```csharp
var activeUsers = context.Users
    .Where(u => u.IsActive)
    .Select(u => new { u.Name, u.Role })
    .ToList();
```  

17. **What is the role of DbContext in EF Core, and how do you configure it?**  
- `DbContext` is the primary class in EF Core for interacting with the database.  
- It manages entity objects, tracks changes, and performs database operations.  
- Configuration includes connection strings and database provider setup in the `OnConfiguring` method or `Startup.cs`.  
- Example: Configured `DbContext` to use SQL Server with a connection string:  

```csharp
services.AddDbContext<ApplicationDbContext>(options =>
    options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));
```  

18. **What are the performance considerations when using EF Core in large-scale systems?**  
- Optimize queries by selecting only necessary fields with projections.  
- Use eager loading or `AsNoTracking` for read-heavy operations to reduce memory overhead.  
- Minimize round trips to the database by batching operations.  
- Example: Improved performance in a reporting system by using projections and eager loading:  

```csharp
var reports = context.Reports
    .Include(r => r.Author)
    .Select(r => new { r.Title, AuthorName = r.Author.Name })
    .ToList();
```  

19. **How do you configure multiple database contexts in a .NET Core application?**  
- Define separate `DbContext` classes for each database schema or purpose.  
- Configure each context in the `Startup.cs` file using different connection strings.  
- Use dependency injection to resolve the appropriate `DbContext` where needed.  
- Example: Configured `UserDbContext` and `OrderDbContext` for separate databases:  

```csharp
services.AddDbContext<UserDbContext>(options =>
    options.UseSqlServer(Configuration.GetConnectionString("UserDb")));
services.AddDbContext<OrderDbContext>(options =>
    options.UseSqlServer(Configuration.GetConnectionString("OrderDb")));
```  
20. **How can you manage concurrency conflicts in EF Core?**  
- Use a concurrency token such as `RowVersion` or `[ConcurrencyCheck]` on specific properties.  
- EF Core detects changes to the concurrency token and throws `DbUpdateConcurrencyException` when conflicts occur.  
- Handle conflicts by retrying, merging changes, or discarding updates based on application logic.  
- Example: Implemented `RowVersion` to track changes in an employee record system:  

```csharp
public class Employee
{
    public int Id { get; set; }
    public string Name { get; set; }
    [Timestamp]
    public byte[] RowVersion { get; set; }
}
```

21. **Explain the difference between FirstOrDefault and SingleOrDefault in LINQ queries.**  
- `FirstOrDefault` retrieves the first matching element or returns `null` if no match is found.  
- `SingleOrDefault` ensures only one element matches the criteria and throws an exception if multiple matches exist.  
- Use `FirstOrDefault` for scenarios where multiple matches are acceptable but only the first is needed.  
- Example: Retrieved a user by email using `SingleOrDefault` to ensure uniqueness:  

```csharp
var user = context.Users.SingleOrDefault(u => u.Email == "user@example.com");
```

22. **How do you handle transactions in EF Core?**  
- Use `DbContext.Database.BeginTransaction` to manually control transactions.  
- Combine operations within the transaction and commit only if all succeed.  
- Rollback the transaction in case of an exception or failure.  
- Example: Implemented a transaction to ensure order creation and payment processing were atomic:  

```csharp
using (var transaction = context.Database.BeginTransaction())
{
    try
    {
        context.Orders.Add(newOrder);
        context.SaveChanges();
        
        context.Payments.Add(newPayment);
        context.SaveChanges();
        
        transaction.Commit();
    }
    catch
    {
        transaction.Rollback();
        throw;
    }
}
```

23. **How can you debug SQL queries generated by EF Core?**  
- Enable logging for EF Core to view generated SQL queries in the output or logs.  
- Use `ToQueryString()` to directly view the SQL for a LINQ query.  
- Tools like SQL Profiler or logging frameworks can also capture and analyze queries.  
- Example: Debugged a slow query by examining its SQL using `ToQueryString()`:  

```csharp
var query = context.Users.Where(u => u.IsActive).ToQueryString();
Console.WriteLine(query);
```  
24. **Explain the use of Owned Entity Types in EF Core.**  
- Owned entity types allow modeling complex types as part of a parent entity rather than as a separate table.  
- These types are configured as value objects and share the table of their owning entity.  
- Use `OwnsOne` in the Fluent API to configure owned entity relationships.  
- Example: Implemented an `Address` type owned by a `Customer` entity:  

```csharp
modelBuilder.Entity<Customer>()
    .OwnsOne(c => c.Address, a =>
    {
        a.Property(p => p.Street).HasColumnName("Street");
        a.Property(p => p.City).HasColumnName("City");
    });
```

25. **What are the advantages and limitations of using EF Core in a high-performance application?**  
- Advantages: Simplifies data access, supports LINQ queries, and provides built-in migration and schema management.  
- Limitations: May generate inefficient SQL for complex queries, and runtime performance may lag raw SQL in high-load scenarios.  
- Mitigation: Optimize queries, disable change tracking for read-heavy workloads, and leverage raw SQL for critical operations.  
- Example: In a high-load e-commerce system, EF Core was optimized using `AsNoTracking` and projections for read-heavy queries.  

```csharp
var products = context.Products.AsNoTracking()
    .Select(p => new { p.Name, p.Price })
    .ToList();
```

26. **How does Entity Framework Core handle shadow properties, and how can they be used effectively?**  
- Shadow properties exist in the model but are not defined in the entity class.  
- Useful for tracking metadata like timestamps or audit fields without modifying domain classes.  
- Configure shadow properties using Fluent API in `OnModelCreating`.  
- Example: Configured `CreatedDate` as a shadow property for auditing:  

```csharp
modelBuilder.Entity<Order>()
    .Property<DateTime>("CreatedDate")
    .HasDefaultValueSql("GETDATE()");
```

27. **How do you configure table splitting in EF Core to map multiple entity types to a single database table?**  
- Use table splitting to map different entity types to shared columns in a single database table.  
- Configure table splitting with `HasOne` and `WithOwner` Fluent API methods.  
- Each entity must have a relationship with a common primary key.  
- Example: Configured `User` and `UserProfile` to share the same table:  

```csharp
modelBuilder.Entity<User>()
    .HasOne(u => u.Profile)
    .WithOwner()
    .HasForeignKey<UserProfile>(p => p.UserId);
```  

28. **What are the benefits and drawbacks of using lazy loading in EF Core?**  
- Benefits: Reduces initial data load and simplifies code by loading related data only when needed.  
- Drawbacks: Increases the risk of N+1 query problems and can negatively impact performance with frequent database calls.  
- Use eager loading or explicit loading where performance is critical.  
- Example: Disabled lazy loading in a project to avoid unintended queries and optimize performance.  

```csharp
services.AddDbContext<ApplicationDbContext>(options =>
    options.UseLazyLoadingProxies(false));
```  

29. **How can you implement soft delete functionality using EF Core's global query filters?**  
- Soft delete involves marking records as inactive instead of physically deleting them.  
- Use global query filters to automatically exclude inactive records from queries.  
- Implement a `IsDeleted` property and configure it as a filter.  
- Example: Configured a global filter for soft deletion in the `OnModelCreating` method:  

```csharp
modelBuilder.Entity<User>().HasQueryFilter(u => !u.IsDeleted);
```  

30. **Explain the difference between DbSet and DbQuery in EF Core and their respective use cases.**  
- `DbSet`: Represents a table in the database and allows CRUD operations.  
- `DbQuery`: Represents a read-only queryable object, often mapped to views or raw SQL.  
- `DbQuery` is suitable for scenarios where data does not have a primary key or is not updated.  
- Example: Used `DbSet` for user management and `DbQuery` for reporting on aggregated data.  

```csharp
public DbSet<User> Users { get; set; }
public DbQuery<UserReport> UserReports { get; set; }
```  

31. **How do you optimize EF Core queries for performance with eager loading, projection, and splitting?**  
- Use eager loading to fetch related data in a single query.  
- Project data to retrieve only required fields and reduce payload size.  
- Split queries to handle complex data loads efficiently.  
- Example: Used projection to reduce overhead in a dashboard query:  

```csharp
var data = context.Users
    .Include(u => u.Orders)
    .Select(u => new { u.Name, TotalOrders = u.Orders.Count })
    .ToList();
```  

32. **What are value objects in EF Core, and how are they different from entities?**  
- Value objects represent concepts with no identity, defined by their properties.  
- Entities have unique identifiers (primary keys) and are tracked by EF Core.  
- Value objects are immutable and often used for small, reusable data structures.  
- Example: Implemented `Address` as a value object in a customer entity:  

```csharp
public class Address
{
    public string Street { get; private set; }
    public string City { get; private set; }
}
```  

33. **How does EF Core support database-first and code-first approaches? Provide examples of each.**  
- Database-First: Reverse-engineers a database schema into entity models using scaffolding.  
- Code-First: Models are defined in code, and EF Core generates the database schema.  
- Example: Scaffolded models from an existing database using the database-first approach:  

```bash
dotnet ef dbcontext scaffold "YourConnectionString" Microsoft.EntityFrameworkCore.SqlServer
```  

34. **How can you use migrations in EF Core to manage schema changes in production environments?**  
- Use migrations to track schema changes and update databases incrementally.  
- Generate scripts using `dotnet ef migrations script` for deployment.  
- Apply scripts carefully in production to avoid downtime or data loss.  
- Example: Deployed a migration script to add a new column in production:  

```bash
dotnet ef migrations add AddNewColumn
dotnet ef database update
```  
### 35. What is EF Core, and how does it differ from EF6?  
- EF Core is a lightweight, extensible, and cross-platform version of Entity Framework.  
- EF6 is a mature, feature-rich framework limited to .NET Framework, whereas EF Core supports .NET Core and .NET 5+.  
- EF Core lacks some features of EF6, like lazy loading proxies by default but adds advanced features like alternate keys, batching, and shadow properties.  
- Example: Migrated an application from EF6 to EF Core to take advantage of cross-platform compatibility and improved performance.  

---

### 36. How do you install and configure EF Core in a .NET Core project?  
- Install EF Core packages for your database provider using NuGet, e.g., `Microsoft.EntityFrameworkCore.SqlServer`.  
- Add a `DbContext` class to define your database context and entities.  
- Configure the database connection in the `OnConfiguring` method or in `Startup.cs` using `AddDbContext`.  
- Example: Installed and configured EF Core with SQL Server in a project:  

```bash
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
```

```csharp
services.AddDbContext<AppDbContext>(options =>
    options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));
```

---

### 37. What are navigation properties in EF Core, and why are they important?  
- Navigation properties define relationships between entities and allow navigation across related data.  
- They can be used to load related data using lazy, eager, or explicit loading.  
- Types include collection navigation (e.g., `ICollection<T>`) and reference navigation (e.g., single entity).  
- Example: Used navigation properties to load orders for a customer:  

```csharp
var customerWithOrders = context.Customers
    .Include(c => c.Orders)
    .FirstOrDefault(c => c.Id == customerId);
```

---

### 38. How do you perform basic CRUD operations in EF Core?  
- **Create**: Add new entities using `Add` or `AddRange` and save changes using `SaveChanges`.  
- **Read**: Use LINQ queries to retrieve data from the database.  
- **Update**: Modify entity properties and call `SaveChanges`.  
- **Delete**: Use `Remove` or `RemoveRange` to delete entities and save changes.  
- Example: Performed CRUD operations in a product management module:  

```csharp
// Create
var product = new Product { Name = "New Product", Price = 100 };
context.Products.Add(product);
context.SaveChanges();

// Read
var productList = context.Products.ToList();

// Update
product.Price = 120;
context.SaveChanges();

// Delete
context.Products.Remove(product);
context.SaveChanges();
```

---

### 39. How does EF Core handle primary keys by default?  
- EF Core expects a property named `Id` or `<EntityName>Id` as the primary key.  
- You can configure a primary key explicitly using the Fluent API or data annotations.  
- Composite keys must be defined using the Fluent API with `HasKey`.  
- Example: Configured a composite primary key for an `Order` entity:  

```csharp
modelBuilder.Entity<Order>()
    .HasKey(o => new { o.OrderId, o.ProductId });
```  

---

### 40. How do you configure composite keys in EF Core using Fluent API?  
- Composite keys are configured using the `HasKey` method in the `OnModelCreating` method.  
- You need to specify multiple properties that together form the key.  
- EF Core does not support composite keys via data annotations.  
- Example: Configured a composite key for a `StudentCourse` junction table:  

```csharp
modelBuilder.Entity<StudentCourse>()
    .HasKey(sc => new { sc.StudentId, sc.CourseId });
```

---

### 41. How do you track changes to entities in EF Core?  
- EF Core uses **Change Tracker** to monitor changes made to entities.  
- Each entity's state (e.g., Added, Modified, Deleted, Unchanged) is tracked by EF Core.  
- Use `context.Entry(entity).State` to inspect or change the state.  
- Example: Checked the state of an updated entity:  

```csharp
var student = context.Students.First();
student.Name = "Updated Name";
var state = context.Entry(student).State; // Outputs EntityState.Modified
```

---

### 42. How do you configure cascading deletes in EF Core?  
- Cascading deletes propagate a delete operation on a parent entity to its dependent entities.  
- Use the Fluent API with `OnDelete` to configure cascading behavior.  
- Options include `Cascade`, `Restrict`, and `SetNull`.  
- Example: Configured cascading delete for a `Student` and their `Enrollments`:  

```csharp
modelBuilder.Entity<Student>()
    .HasMany(s => s.Enrollments)
    .WithOne(e => e.Student)
    .OnDelete(DeleteBehavior.Cascade);
```

---

### 43. What is the difference between `Include` and `ThenInclude` in EF Core?  
- `Include`: Used to load related data for a single level of navigation property.  
- `ThenInclude`: Used to load further related data for a property of a related entity.  
- Both are essential for eager loading in EF Core.  
- Example: Used `Include` and `ThenInclude` to fetch a nested relationship:  

```csharp
var data = context.Orders
    .Include(o => o.Customer)
    .ThenInclude(c => c.Address)
    .ToList();
```

---

### 44. What is the difference between `Add`, `Update`, and `Attach` methods in EF Core?  
- `Add`: Marks an entity as `Added` to be inserted into the database on `SaveChanges`.  
- `Update`: Marks an entity as `Modified`, ensuring all properties are updated.  
- `Attach`: Tracks an entity without marking it as modified (used for disconnected scenarios).  
- Example: Attached an entity to update only specific properties:  

```csharp
context.Attach(existingUser);
existingUser.Email = "newemail@example.com";
context.SaveChanges();
```

---

### 45. How do you seed initial data in EF Core?  
- Seed data using the `HasData` method in `OnModelCreating`.  
- This ensures predefined data is inserted during migrations.  
- Use this for static data like roles, countries, or initial users.  
- Example: Seeded initial roles in a system:  

```csharp
modelBuilder.Entity<Role>().HasData(
    new Role { Id = 1, Name = "Admin" },
    new Role { Id = 2, Name = "User" }
);
```  
### 46. What are query types in EF Core, and how do they differ from entity types?  
- Query types are used for non-entity types, such as views or raw SQL queries, that do not have primary keys.  
- They are read-only and cannot track changes or support CRUD operations.  
- Useful for fetching data not mapped to a database table.  
- Example: Mapped a query type to a SQL view:  

```csharp
modelBuilder.Query<SalesReport>()
    .ToView("View_SalesReport");
```

---

### 47. How does EF Core support disconnected scenarios?  
- In disconnected scenarios, entities are detached from the context, typically during client-server interactions.  
- EF Core allows reattaching entities using `Attach` or `Update`.  
- Use change tracking to maintain state transitions effectively.  
- Example: Updated a disconnected entity in a web application:  

```csharp
context.Attach(updatedEntity);
context.Entry(updatedEntity).State = EntityState.Modified;
context.SaveChanges();
```

---

### 48. What are alternate keys in EF Core, and when should they be used?  
- Alternate keys are unique constraints other than the primary key.  
- They are useful for enforcing uniqueness on columns like email or username.  
- Configure them using the Fluent API with `HasAlternateKey`.  
- Example: Added an alternate key for a `User` entity's `Email` property:  

```csharp
modelBuilder.Entity<User>()
    .HasAlternateKey(u => u.Email);
```

---

### 49. How can EF Core handle hierarchical data structures?  
- Model hierarchical relationships using self-referencing navigation properties.  
- Use Fluent API to configure relationships explicitly.  
- Load hierarchical data using recursive queries or eager loading.  
- Example: Configured a `Category` entity with a parent-child relationship:  

```csharp
modelBuilder.Entity<Category>()
    .HasOne(c => c.Parent)
    .WithMany(c => c.Children)
    .HasForeignKey(c => c.ParentId);
```

---

### 50. What is the role of value converters in EF Core?  
- Value converters allow transforming property values when reading from or writing to the database.  
- Useful for handling custom types or encrypted data.  
- Configure them in `OnModelCreating` using `HasConversion`.  
- Example: Converted an `enum` to a string column:  

```csharp
modelBuilder.Entity<Order>()
    .Property(o => o.Status)
    .HasConversion<string>();
```

---

### 51. How do you configure a default schema for a database in EF Core?  
- Set a default schema globally using the Fluent API in `OnModelCreating`.  
- This applies to all entities unless explicitly overridden.  
- Useful for multi-tenant or organized database setups.  
- Example: Configured a default schema for an application:  

```csharp
modelBuilder.HasDefaultSchema("Sales");
```

---

### 52. What are keyless entities in EF Core, and how are they used?  
- Keyless entities are entities without a primary key.  
- They are used for read-only queries, like mapping database views or raw SQL results.  
- Configure them using the Fluent API with `HasNoKey`.  
- Example: Defined a keyless entity for a view:  

```csharp
modelBuilder.Entity<SalesReport>()
    .HasNoKey();
```

---

### 53. How does EF Core support enum mapping to database columns?  
- Enums can be directly mapped to integer columns by default.  
- Alternatively, map enums to strings using value converters.  
- Use `HasConversion` to customize the mapping.  
- Example: Mapped an `OrderStatus` enum to a string:  

```csharp
modelBuilder.Entity<Order>()
    .Property(o => o.Status)
    .HasConversion(
        v => v.ToString(),
        v => (OrderStatus)Enum.Parse(typeof(OrderStatus), v));
```

---

### 54. How can you use database functions in EF Core queries?  
- EF Core allows using database functions like `LEN`, `LOWER`, or custom functions in LINQ queries.  
- Use `EF.Functions` for built-in functions or `HasDbFunction` for custom functions.  
- Example: Used `LEN` function in a query:  

```csharp
var result = context.Users
    .Where(u => EF.Functions.Like(u.Name, "%John%"))
    .ToList();
```

---

### 55. How does EF Core handle pessimistic and optimistic concurrency?  
- Optimistic concurrency: Uses a concurrency token, like a timestamp, to detect conflicts.  
- Pessimistic concurrency: Locks a database row during updates to prevent conflicts.  
- EF Core natively supports optimistic concurrency using `RowVersion` or similar fields.  
- Example: Configured a concurrency token in an entity:  

```csharp
modelBuilder.Entity<Product>()
    .Property(p => p.RowVersion)
    .IsRowVersion();
```

---

### 56. What are table-per-hierarchy (TPH) and table-per-type (TPT) inheritance strategies in EF Core?  
- **TPH**: All derived types share a single table with a discriminator column.  
- **TPT**: Each derived type has its own table with relationships to the base type.  
- Use Fluent API to configure inheritance strategies.  
- Example: Configured TPH inheritance for a `Shape` hierarchy:  

```csharp
modelBuilder.Entity<Shape>()
    .HasDiscriminator<string>("ShapeType")
    .HasValue<Circle>("Circle")
    .HasValue<Square>("Square");
```

---

### 57. How do you configure computed columns in EF Core?  
- Computed columns are database columns whose values are calculated by the database.  
- Use the Fluent API to define computed columns.  
- Useful for columns derived from other columns, like totals or timestamps.  
- Example: Configured a `FullName` computed column:  

```csharp
modelBuilder.Entity<User>()
    .Property(u => u.FullName)
    .HasComputedColumnSql("[FirstName] + ' ' + [LastName]");
```

---

### 58. How can you track raw SQL queries in EF Core for debugging?  
- Use EF Core’s `ToQueryString` to inspect the generated SQL for LINQ queries.  
- Use logging frameworks to log SQL commands executed by EF Core.  
- Enable detailed logs in the `DbContext` options configuration.  
- Example: Debugged a raw SQL query:  

```csharp
var query = context.Users.Where(u => u.Age > 30);
Console.WriteLine(query.ToQueryString());
```

---

### 59. What are shadow foreign keys, and how are they used in EF Core?  
- Shadow foreign keys are keys not explicitly defined in the entity class but used for relationships.  
- EF Core creates them automatically when navigation properties are defined.  
- Access them using `EF.Property` in queries or configurations.  
- Example: Used a shadow foreign key in a query:  

```csharp
var students = context.Students
    .Where(s => EF.Property<int>(s, "CourseId") == 1)
    .ToList();
```

---

### 60. How does EF Core support partitioned tables?  
- EF Core doesn’t natively manage partitioning but supports querying partitioned tables created in the database.  
- Use Fluent API or SQL for partition-specific configurations.  
- Optimize queries by targeting partitions directly in raw SQL.  
- Example: Queried a partitioned table using raw SQL:  

```csharp
var data = context.Customers
    .FromSqlRaw("SELECT * FROM PartitionedTable WHERE PartitionKey = 2024")
    .ToList();
```  

### 61. How do you map a one-to-many relationship using Fluent API in EF Core?  
- Define a `HasMany` relationship in the parent entity and `WithOne` in the child entity.  
- Specify the foreign key using `HasForeignKey`.  
- Use navigation properties for bidirectional or unidirectional relationships.  
- Example: Configured a one-to-many relationship for `Order` and `OrderItem`:  

```csharp
modelBuilder.Entity<Order>()
    .HasMany(o => o.OrderItems)
    .WithOne(oi => oi.Order)
    .HasForeignKey(oi => oi.OrderId);
```

---

### 62. How does EF Core support splitting queries for performance optimization?  
- Splitting queries reduces the SQL query complexity for loading related data.  
- Configure it using `AsSplitQuery` in LINQ for related entities.  
- Improves performance by breaking large joins into smaller queries.  
- Example: Split query for loading orders and their details:  

```csharp
var orders = context.Orders
    .Include(o => o.OrderDetails)
    .AsSplitQuery()
    .ToList();
```

---

### 63. What is the purpose of global query filters in EF Core?  
- Global query filters define a condition applied to all queries on an entity.  
- Useful for implementing multi-tenancy, soft deletes, or security filters.  
- Defined in `OnModelCreating` using the Fluent API.  
- Example: Added a global filter for soft-delete functionality:  

```csharp
modelBuilder.Entity<Product>()
    .HasQueryFilter(p => !p.IsDeleted);
```

---

### 64. How do you handle many-to-many relationships in EF Core?  
- Define a join table implicitly by navigation properties or explicitly with an entity class.  
- Configure the relationship using `HasMany` and `WithMany`.  
- For explicit join entities, configure the primary key in the join table.  
- Example: Configured a many-to-many relationship for `Student` and `Course`:  

```csharp
modelBuilder.Entity<Student>()
    .HasMany(s => s.Courses)
    .WithMany(c => c.Students)
    .UsingEntity<Enrollment>(
        j => j.HasOne(e => e.Course).WithMany(c => c.Enrollments),
        j => j.HasOne(e => e.Student).WithMany(s => s.Enrollments));
```

---

### 65. How does EF Core handle value objects, and what are they?  
- Value objects are immutable objects that represent a concept, not a unique identity (e.g., `Address`).  
- Configured using owned types in EF Core with `OwnsOne`.  
- Changes to value objects require replacing the entire object.  
- Example: Configured an owned type for `Address`:  

```csharp
modelBuilder.Entity<Customer>()
    .OwnsOne(c => c.Address, a =>
    {
        a.Property(ad => ad.Street).HasColumnName("StreetName");
    });
```

---

### 66. What is the role of database providers in EF Core?  
- Database providers enable EF Core to work with different databases (e.g., SQL Server, PostgreSQL, SQLite).  
- You install the provider package to enable support for the chosen database.  
- Providers extend EF Core functionality specific to the database.  
- Example: Used `Microsoft.EntityFrameworkCore.SqlServer` for SQL Server in a project.  

---

### 67. How do you implement soft delete in EF Core?  
- Use a boolean property like `IsDeleted` in the entity class.  
- Apply a global query filter to exclude soft-deleted records.  
- Update the `IsDeleted` flag instead of deleting the record.  
- Example: Configured soft delete for a `Product` entity:  

```csharp
modelBuilder.Entity<Product>()
    .HasQueryFilter(p => !p.IsDeleted);
```

---

### 68. How does EF Core support spatial data types?  
- EF Core supports spatial data like geography and geometry types through extensions like `NetTopologySuite`.  
- Configure it by adding the spatial data package for your database provider.  
- Use spatial methods such as distance calculations in LINQ.  
- Example: Queried entities based on spatial distance:  

```csharp
var nearbyLocations = context.Locations
    .Where(l => l.Location.Distance(targetLocation) < 1000)
    .ToList();
```

---

### 69. How can EF Core integrate with database views?  
- Map a database view to an entity using the Fluent API with `ToView`.  
- Views are read-only unless explicitly mapped with appropriate configurations.  
- Useful for fetching aggregated or complex data.  
- Example: Mapped a `SalesReport` view to an entity:  

```csharp
modelBuilder.Entity<SalesReport>()
    .ToView("View_SalesReport");
```

---

### 70. How do you configure alternate schemas for entities in EF Core?  
- Specify a schema for an entity using the Fluent API with `ToTable`.  
- This allows organizing entities across different schemas.  
- Default schema configuration can also be applied globally.  
- Example: Configured a `Product` entity in the `Inventory` schema:  

```csharp
modelBuilder.Entity<Product>()
    .ToTable("Products", schema: "Inventory");
```

---

### 71. How does EF Core support raw SQL queries with parameterization?  
- Execute raw SQL using `FromSql` or `ExecuteSqlRaw` with parameters.  
- Parameterized queries prevent SQL injection.  
- Suitable for complex queries not supported by LINQ.  
- Example: Queried data with raw SQL and parameters:  

```csharp
var products = context.Products
    .FromSqlRaw("SELECT * FROM Products WHERE Price > {0}", 50)
    .ToList();
```

---

### 72. How do you configure table splitting in EF Core?  
- Table splitting maps multiple entities to a single table.  
- Configure it using the Fluent API with `ToTable` and `HasOne`.  
- Useful for optimizing data storage and relationships.  
- Example: Configured table splitting for `Person` and `PersonDetail`:  

```csharp
modelBuilder.Entity<Person>()
    .ToTable("People")
    .HasOne(p => p.PersonDetail)
    .WithOne(pd => pd.Person)
    .HasForeignKey<PersonDetail>(pd => pd.PersonId);
```

---

### 73. What are the limitations of using EF Core with large-scale systems?  
- Performance can degrade with large datasets if not optimized (e.g., lazy loading).  
- Migrations may become cumbersome with complex schemas.  
- Query generation may not always match handcrafted SQL.  
- Example: Optimized EF Core by splitting queries and using stored procedures for critical operations.  

---

### 74. How does EF Core handle shadow properties, and what are they used for?  
- Shadow properties are properties not defined in the entity class but tracked by EF Core.  
- Used for metadata like foreign keys or audit fields (e.g., `CreatedAt`).  
- Access shadow properties using `EF.Property`.  
- Example: Queried using a shadow property for `CreatedAt`:  

```csharp
var recentUsers = context.Users
    .Where(u => EF.Property<DateTime>(u, "CreatedAt") > DateTime.Now.AddDays(-7))
    .ToList();
```  

---

### 75. What is entity splitting, and how do you implement it in EF Core?  
- Entity splitting maps different properties of an entity to separate tables.  
- Useful for organizing large entities into manageable pieces.  
- Configure it using Fluent API with `ToTable`.  
- Example: Split a `User` entity into `User` and `UserDetails` tables:  

```csharp
modelBuilder.Entity<User>()
    .ToTable("Users")
    .Property(u => u.Id).IsRequired();

modelBuilder.Entity<User>()
    .ToTable("UserDetails")
    .Property(u => u.Address).IsRequired();
```  
### 76. How does EF Core handle cascade delete, and how can it be configured?  
- Cascade delete automatically deletes dependent entities when a principal entity is removed.  
- Configure cascade behavior using `OnDelete` in the Fluent API.  
- Supported behaviors include `Cascade`, `SetNull`, and `Restrict`.  
- Example: Configured cascade delete for `Order` and `OrderItem`:  

```csharp
modelBuilder.Entity<Order>()
    .HasMany(o => o.OrderItems)
    .WithOne(oi => oi.Order)
    .OnDelete(DeleteBehavior.Cascade);
```

---

### 77. How can you create custom conventions in EF Core?  
- Custom conventions apply specific configurations globally to entities or properties.  
- Use `IModelFinalizingConvention` or configure in `OnModelCreating`.  
- Useful for enforcing uniform naming or validation rules.  
- Example: Configured a custom convention for table names:  

```csharp
foreach (var entity in modelBuilder.Model.GetEntityTypes())
{
    modelBuilder.Entity(entity.Name).ToTable(entity.GetTableName().ToLower());
}
```

---

### 78. How does EF Core handle data seeding, and how can it be implemented?  
- Data seeding populates the database with initial or default data during migrations.  
- Define seed data in `OnModelCreating` using `HasData`.  
- Seeded data is included in migration scripts.  
- Example: Seeded an admin user into the `Users` table:  

```csharp
modelBuilder.Entity<User>().HasData(
    new User { Id = 1, Name = "Admin", Role = "Administrator" }
);
```

---

### 79. How do you handle JSON columns in EF Core?  
- JSON columns are supported through providers like PostgreSQL or SQL Server.  
- Map a property to a JSON column using Fluent API.  
- Useful for storing structured data in a single column.  
- Example: Mapped a JSON column for `OrderDetails`:  

```csharp
modelBuilder.Entity<Order>()
    .Property(o => o.OrderDetails)
    .HasColumnType("jsonb");
```

---

### 80. What are owned entity types, and how do you configure them in EF Core?  
- Owned types represent value objects owned by a single entity.  
- Configure using `OwnsOne` in the Fluent API.  
- Stored in the same table as the owning entity by default.  
- Example: Configured an owned `Address` type for a `Customer`:  

```csharp
modelBuilder.Entity<Customer>()
    .OwnsOne(c => c.Address, a =>
    {
        a.Property(ad => ad.City).HasColumnName("City");
    });
```

---

### 81. How does EF Core handle default values for columns?  
- Default values can be set for columns using `HasDefaultValue` or `HasDefaultValueSql`.  
- Useful for timestamps, GUIDs, or predefined constants.  
- Defaults are applied during insertion if a value is not provided.  
- Example: Configured a default value for `CreatedAt`:  

```csharp
modelBuilder.Entity<User>()
    .Property(u => u.CreatedAt)
    .HasDefaultValueSql("GETDATE()");
```

---

### 82. What are the benefits and limitations of shadow properties in EF Core?  
- **Benefits**: Simplifies entity models by avoiding explicit property definitions.  
- **Limitations**: Harder to query and debug since they are not in the entity class.  
- Example: Accessed a shadow property in a LINQ query:  

```csharp
var recentOrders = context.Orders
    .Where(o => EF.Property<DateTime>(o, "CreatedAt") > DateTime.UtcNow.AddDays(-7))
    .ToList();
```

---

### 83. How do you map composite keys in EF Core?  
- Composite keys combine multiple properties as a primary key.  
- Configure using the Fluent API with `HasKey`.  
- Example: Configured a composite key for `Order` and `Product` in `OrderDetail`:  

```csharp
modelBuilder.Entity<OrderDetail>()
    .HasKey(od => new { od.OrderId, od.ProductId });
```

---

### 84. How does EF Core support raw SQL queries with projections?  
- Use `FromSql` with projections to map raw SQL query results to DTOs or anonymous types.  
- Useful for optimizing queries or fetching non-entity data.  
- Example: Fetched data into a DTO using raw SQL:  

```csharp
var salesData = context.SalesReports
    .FromSqlRaw("SELECT ProductName, SUM(Sales) AS TotalSales FROM Sales GROUP BY ProductName")
    .ToList();
```

---

### 85. How do you handle composite foreign keys in EF Core?  
- Composite foreign keys map multiple properties as a foreign key.  
- Configure using Fluent API with `HasForeignKey`.  
- Example: Configured a composite foreign key in `OrderDetail`:  

```csharp
modelBuilder.Entity<OrderDetail>()
    .HasOne(od => od.Product)
    .WithMany(p => p.OrderDetails)
    .HasForeignKey(od => new { od.OrderId, od.ProductId });
```

---

### 86. How does EF Core handle transaction management?  
- EF Core supports transactions with `BeginTransaction`, `Commit`, and `Rollback`.  
- Use `DbContextTransaction` for explicit control or `TransactionScope` for distributed transactions.  
- Example: Handled a transaction to update multiple entities:  

```csharp
using var transaction = context.Database.BeginTransaction();
try
{
    context.Users.Add(new User { Name = "John" });
    context.SaveChanges();

    context.Orders.Add(new Order { UserId = 1, Total = 100 });
    context.SaveChanges();

    transaction.Commit();
}
catch
{
    transaction.Rollback();
}
```

---

### 87. How do you optimize performance in EF Core for large datasets?  
- Use projection to reduce data size in queries.  
- Avoid unnecessary `Include` for navigation properties.  
- Use compiled queries for frequently used LINQ queries.  
- Example: Used a compiled query for better performance:  

```csharp
var compiledQuery = EF.CompileQuery((MyDbContext ctx, int age) =>
    ctx.Users.Where(u => u.Age > age));
var result = compiledQuery(context, 30);
```

---

### 88. How can you map entities to database functions in EF Core?  
- Map database functions using `HasDbFunction` in `OnModelCreating`.  
- Use them in LINQ queries as custom methods.  
- Example: Mapped a database function for calculating discounts:  

```csharp
modelBuilder.HasDbFunction(() => MyDbContext.CalculateDiscount(0))
    .HasName("CalculateDiscount");
```

---

### 89. What are split entities in EF Core, and how do they improve storage?  
- Split entities map different sets of properties to separate tables.  
- Useful for large entities with optional or infrequently used properties.  
- Example: Split a `User` entity into two tables:  

```csharp
modelBuilder.Entity<User>().SplitToTable(
    "Users", u => new { u.Id, u.Name },
    "UserDetails", ud => new { ud.Id, ud.Address });
```

---

### 90. How does EF Core support temporal tables?  
- Temporal tables track changes over time, storing historical data.  
- Enable using the Fluent API and include `PeriodStart` and `PeriodEnd`.  
- Example: Configured a temporal table for `Orders`:  

```csharp
modelBuilder.Entity<Order>()
    .ToTable("Orders", table => table.IsTemporal());
```
