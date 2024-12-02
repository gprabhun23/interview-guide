### **1. Is it possible to rename a database? If so, how would you rename the database?**  
- Yes, it is possible to rename a database in SQL Server.  
- You can use the `ALTER DATABASE` command or the SQL Server Management Studio (SSMS) interface.  
- The database must be in a state where no connections are active, and it should not be involved in replication.  
- Example:  
```sql
ALTER DATABASE OldDatabaseName MODIFY NAME = NewDatabaseName;
-- I used this command during a database migration to reflect the updated naming convention.
```

### **2. What is TOP in T-SQL?**  
- `TOP` is used to limit the number of rows returned by a query.  
- It works with SELECT, INSERT INTO, and DELETE operations.  
- You can specify a fixed number or a percentage of rows using `TOP (n)` or `TOP (n) PERCENT`.  
- Example:  
```sql
SELECT TOP (5) * FROM Employees ORDER BY Salary DESC;
-- I used this to extract the top 5 highest-paid employees from an employee table.
```

### **3. What are T-SQL Window functions?**  
- Window functions perform calculations across a set of table rows related to the current row.  
- These include `ROW_NUMBER`, `RANK`, `DENSE_RANK`, and `NTILE`.  
- They are often used with the `OVER` clause for partitioning or ordering.  
- Example:  
```sql
SELECT Name, Salary, RANK() OVER (PARTITION BY Department ORDER BY Salary DESC) AS Rank
FROM Employees;
-- I applied window functions in a performance dashboard to rank employees within departments.
```

### **4. When should I use a primary key or an index?**  
- Use a primary key to uniquely identify each row in a table.  
- Use an index to improve the performance of queries.  
- Primary keys automatically create a unique clustered index unless specified otherwise.  
- Example:  
```sql
CREATE INDEX idx_employee_name ON Employees (Name);
-- I created an index to speed up searches on employee names in a large database.
```

### **5. Could you explain the difference between Primary Key and Unique Index?**  
- A primary key enforces both uniqueness and the "not null" constraint.  
- A unique index ensures uniqueness but allows multiple nulls.  
- Each table can have only one primary key but multiple unique indexes.  
- Example:  
```sql
-- Primary Key
CREATE TABLE Products (ID INT PRIMARY KEY, Name NVARCHAR(50));

-- Unique Index
CREATE UNIQUE INDEX idx_unique_email ON Customers (Email);
-- I used unique indexes to enforce email uniqueness without making it a primary key.
```

### **6. What are the three ways that Dynamic SQL can be issued?**  
- Using `EXEC` to execute a query string directly.  
- Using `sp_executesql` for parameterized dynamic SQL.  
- Generating and running the dynamic query with application logic.  
- Example:  
```sql
DECLARE @SQL NVARCHAR(MAX) = 'SELECT * FROM ' + QUOTENAME(@TableName);
EXEC sp_executesql @SQL;
-- I used dynamic SQL to create flexible reports where table names were input dynamically.
```

### **7. What are the new error handling commands introduced with SQL Server 2005 and beyond?**  
- `TRY...CATCH` for structured error handling.  
- `THROW` to re-raise errors with custom messages.  
- Enhanced `ERROR_NUMBER`, `ERROR_MESSAGE`, and other error functions.  
- Example:  
```sql
BEGIN TRY
    INSERT INTO Orders (ID, OrderDate) VALUES (1, NULL);
END TRY
BEGIN CATCH
    PRINT ERROR_MESSAGE();
END CATCH;
-- I implemented TRY...CATCH to log failed transactions into an error log table.
```

### **8. Name 5 commands that can be used to manipulate text in T-SQL.**  
- `LEN`, `CHARINDEX`, `LEFT`, `RIGHT`, and `REPLACE` are commonly used.  
- These commands help in finding, extracting, and replacing text.  
- They are vital for ETL tasks and handling unstructured data.  
- Example:  
```sql
SELECT REPLACE('SQL Server', 'Server', 'Database') AS ModifiedText;
-- I used these functions in a project for cleaning and formatting customer names.
```

### **9. What are the two commands to remove all of the data from a table? Are there any implications with the specific commands?**  
- `TRUNCATE` and `DELETE` can remove all rows.  
- `TRUNCATE` is faster and resets identity columns but doesn't log individual row deletions.  
- `DELETE` logs row deletions and can include conditions.  
- Example:  
```sql
DELETE FROM Employees WHERE Department = 'HR';
TRUNCATE TABLE TempLogs;
-- I used TRUNCATE to quickly clean up staging tables in a data warehouse project.
```

### **10. What is a Subquery in T-SQL?**  
- A subquery is a query nested inside another query.  
- It can return scalar, column, or table data.  
- Subqueries can be used in `SELECT`, `FROM`, or `WHERE` clauses.  
- Example:  
```sql
SELECT Name FROM Employees WHERE DepartmentID = (SELECT ID FROM Departments WHERE Name = 'HR');
-- I used subqueries in a project to filter data based on dynamic criteria.
```

### **11. What are the differences between SQL and T-SQL?**  
- SQL is a standard query language; T-SQL is Microsoft’s extension of SQL.  
- T-SQL includes procedural programming constructs like variables and loops.  
- T-SQL supports advanced features like error handling and window functions.  
- Example:  
```sql
DECLARE @Message NVARCHAR(50) = 'Hello T-SQL';
PRINT @Message;
-- T-SQL features like variables helped me automate tasks in ETL processes.
```

### **12. What is the difference between Data Definition Language (DDL) and Data Manipulation Language (DML)?**  
- DDL deals with schema creation and modification (`CREATE`, `ALTER`, `DROP`).  
- DML handles data operations like `SELECT`, `INSERT`, `UPDATE`, and `DELETE`.  
- DDL changes are auto-committed, while DML can be transactional.  
- Example:  
```sql
-- DDL
CREATE TABLE Employees (ID INT, Name NVARCHAR(50));

-- DML
INSERT INTO Employees VALUES (1, 'John Doe');
-- I used DDL and DML extensively during schema and data migrations.
```

### **13. What are the limitations of the IDENTITY column?**  
- Cannot be updated once set.  
- Sequential values can have gaps if transactions fail.  
- Only one IDENTITY column per table is allowed.  
- Example:  
```sql
CREATE TABLE Orders (OrderID INT IDENTITY(1,1), OrderDate DATE);
-- I faced gaps in IDENTITY columns when handling high transaction volumes and resolved them using SEQUENCE.
```

### **14. What is Blocking in SQL?**  
- Blocking occurs when one transaction locks resources, preventing other transactions from accessing them.  
- It is temporary and resolved once the locking transaction completes.  
- Excessive blocking impacts system performance.  
- Example:  
```sql
-- Identify blocking
EXEC sp_who2;
-- I addressed blocking by optimizing queries and reducing transaction time in critical systems.
```

### **15. What is the OFFSET-FETCH filter in T-SQL?**  
- Used for pagination by skipping and fetching specific rows.  
- Available in SQL Server 2012 and later.  
- Works with `ORDER BY` to ensure predictable results.  
- Example:  
```sql
SELECT * FROM Employees ORDER BY Name OFFSET 10 ROWS FETCH NEXT 5 ROWS ONLY;
-- I used OFFSET-FETCH to implement server-side paging in web applications.
```

### **16. What’s the difference between a Local Temp Table and a Global Temp Table?**  
- Local temp tables (`#TempTable`) are visible only within the session that created them.  
- Global temp tables (`##TempTable`) are visible to all sessions but are deleted once all sessions using them are closed.  
- Local temp tables are ideal for session-specific operations, while global temp tables work well for shared data between sessions.  
- Example:  
```sql
-- Local Temp Table
CREATE TABLE #TempTable (ID INT, Name NVARCHAR(50));
INSERT INTO #TempTable VALUES (1, 'John');

-- Global Temp Table
CREATE TABLE ##TempTable (ID INT, Name NVARCHAR(50));
INSERT INTO ##TempTable VALUES (1, 'John');
-- I used local temp tables during complex data transformations in a stored procedure.
```

### **17. In what version of SQL Server were synonyms released, what do synonyms do, and when could you make the case for using them?**  
- Synonyms were introduced in SQL Server 2005.  
- They provide an alias for database objects like tables, views, or stored procedures.  
- Synonyms simplify cross-database queries and improve code portability.  
- Example:  
```sql
CREATE SYNONYM SalesTable FOR [SalesDB].[dbo].[Orders];
SELECT * FROM SalesTable;
-- I used synonyms to simplify queries in applications accessing multiple databases.
```

### **18. What are bitwise operators and what is the value from a database design perspective?**  
- Bitwise operators like `&`, `|`, `^`, and `~` perform operations at the bit level.  
- They are used for flags or binary data manipulation.  
- They allow compact storage of multiple boolean states.  
- Example:  
```sql
SELECT 5 & 3 AS BitwiseAnd, 5 | 3 AS BitwiseOr;
-- I used bitwise operations to store and retrieve user permissions efficiently.
```

### **19. What are uncommittable transactions?**  
- A transaction enters an uncommittable state when it encounters an error after the `BEGIN TRANSACTION`.  
- In this state, the transaction cannot be committed but must be rolled back.  
- Error handling, like `TRY...CATCH`, is crucial to manage such cases.  
- Example:  
```sql
BEGIN TRANSACTION
UPDATE Orders SET OrderDate = NULL WHERE ID = 1; -- This causes an error
IF @@TRANCOUNT > 0 ROLLBACK TRANSACTION;
-- I encountered uncommittable transactions during bulk updates and handled them with rollback logic.
```

### **20. What’s the difference between Azure SQL Database and Azure SQL Managed Instance?**  
- Azure SQL Database is a fully managed PaaS offering for single databases or elastic pools.  
- Azure SQL Managed Instance offers near-complete SQL Server compatibility with managed features.  
- Managed Instance supports SQL Server Agent and cross-database queries, unlike Azure SQL Database.  
- Example:  
```sql
-- Migration scenario
-- I used Azure SQL Database for lightweight applications and Managed Instance for lifting legacy SQL Server workloads.
```

### **21. What does the T-SQL command IDENT_CURRENT do?**  
- `IDENT_CURRENT` returns the last identity value generated for a specified table, regardless of session or scope.  
- Unlike `@@IDENTITY`, it is table-specific.  
- Careful use is required in concurrent environments to avoid misleading results.  
- Example:  
```sql
SELECT IDENT_CURRENT('Orders') AS LastOrderID;
-- I used this command to track the last inserted ID in audit processes.
```

### **22. What are the practical differences between COALESCE() and ISNULL() in T-SQL?**  
- `COALESCE()` supports multiple arguments and returns the first non-null value.  
- `ISNULL()` accepts only two arguments and returns a replacement for a single null.  
- `COALESCE()` conforms to the ANSI SQL standard, while `ISNULL()` is T-SQL-specific.  
- Example:  
```sql
SELECT COALESCE(NULL, 'Default') AS CoalesceResult, ISNULL(NULL, 'Default') AS IsNullResult;
-- I used COALESCE in reporting to handle multiple fallback values.
```

### **23. Is there a difference between T-SQL linked server and a synonym?**  
- A linked server connects SQL Server to external data sources, enabling cross-server queries.  
- A synonym is a local alias for database objects and does not connect to external servers.  
- Linked servers are for interoperability, while synonyms improve object accessibility.  
- Example:  
```sql
-- Linked Server
SELECT * FROM [LinkedServer].[Database].[Schema].[Table];

-- Synonym
CREATE SYNONYM LocalTable FOR [LinkedServer].[Database].[Schema].[Table];
SELECT * FROM LocalTable;
-- I used linked servers for ETL processes and synonyms for simplifying application queries.
```

### **24. What are the Join Types in T-SQL?**  
- Inner Join: Retrieves matching rows from both tables.  
- Left Join: Retrieves all rows from the left table and matching rows from the right table.  
- Right Join: Retrieves all rows from the right table and matching rows from the left table.  
- Full Join: Retrieves all rows when there’s a match in either table.  
- Example:  
```sql
SELECT e.Name, d.Name AS Department
FROM Employees e
LEFT JOIN Departments d ON e.DepartmentID = d.ID;
-- I used joins extensively for consolidating relational data in reporting systems.
```

### **25. What are the types of XML indexes in SQL Server?**  
- Primary XML Index: Required for creating other XML indexes.  
- Secondary XML Indexes: Includes PATH, VALUE, and PROPERTY indexes for specific query patterns.  
- These indexes improve the performance of XML data retrieval.  
- Example:  
```sql
CREATE PRIMARY XML INDEX px_index ON Products(XmlData);
CREATE SECONDARY XML INDEX sx_path ON Products(XmlData) USING XML INDEX px_index FOR PATH;
-- I applied XML indexes for efficient querying of XML-based configuration data.
```

### **26. What two commands were released in SQL Server 2005 related to comparing data sets from two or more separate SELECT statements?**  
- `EXCEPT`: Returns rows from the first query that are not in the second query.  
- `INTERSECT`: Returns rows common to both queries.  
- They simplify comparing datasets without using `JOIN` or `NOT IN`.  
- Example:  
```sql
SELECT Name FROM Employees
EXCEPT
SELECT Name FROM FormerEmployees;

SELECT Name FROM Employees
INTERSECT
SELECT Name FROM ProjectMembers;
-- I used these commands for data reconciliation in migration projects.
```

### **27. What are ROLLUP and CUBE in T-SQL?**  
- `ROLLUP`: Generates subtotals and a grand total for a hierarchical group.  
- `CUBE`: Generates subtotals and a grand total for all possible combinations of groups.  
- Both are used in `GROUP BY` for advanced aggregation.  
- Example:  
```sql
SELECT Department, SUM(Salary) AS TotalSalary
FROM Employees
GROUP BY ROLLUP(Department);
-- I used ROLLUP to create summary reports for hierarchical data structures.
```

### **28. How can you delete duplicate records in a table with no primary key?**  
- Use `ROW_NUMBER()` with a `CTE` to identify duplicates.  
- Delete rows where `ROW_NUMBER` > 1.  
- Ensure proper ordering to retain the desired record.  
- Example:  
```sql
WITH CTE AS (
    SELECT *, ROW_NUMBER() OVER (PARTITION BY Name ORDER BY ID) AS RowNum
    FROM Employees
)
DELETE FROM CTE WHERE RowNum > 1;
-- I used this method for cleaning legacy data in a customer table.
```

### **29. How do I perform an IF…THEN in a SQL SELECT statement?**  
- Use a `CASE` statement within the `SELECT` clause.  
- It provides conditional logic to transform data dynamically.  
- Simplifies conditional column values or derived calculations.  
- Example:  
```sql
SELECT Name, 
       CASE WHEN Salary > 50000 THEN 'High' ELSE 'Low' END AS SalaryCategory
FROM Employees;
-- I used CASE for categorizing employee salary ranges in reports.
```

### **30. What are the advantages of using Stored Procedures in SQL Server?**  
- Precompiled execution improves performance.  
- Reusability simplifies code management and reduces redundancy.  
- Security enhances by encapsulating business logic.  
- Example:  
```sql
CREATE PROCEDURE GetEmployeeDetails
    @EmployeeID INT
AS
BEGIN
    SELECT * FROM Employees WHERE ID = @EmployeeID;
END;
-- I used stored procedures for consistent and secure data access in a multi-tier application.
```

### **31. What's the difference between TRUNCATE and DELETE in SQL?**  
- `TRUNCATE` removes all rows from a table and resets identity columns.  
- `DELETE` removes rows one by one and logs each deletion.  
- `TRUNCATE` cannot include a `WHERE` clause, while `DELETE` can.  
- Example:  
```sql
DELETE FROM Employees WHERE Department = 'HR';  
TRUNCATE TABLE TempLogs;  
-- I used TRUNCATE to quickly clean up staging tables and DELETE for selective row removal.
```

### **32. What is a Cursor and how does it work?**  
- A cursor allows row-by-row processing of query results.  
- It supports operations like FETCH, UPDATE, or DELETE on individual rows.  
- Cursors are less efficient than set-based operations and should be used sparingly.  
- Example:  
```sql
DECLARE EmployeeCursor CURSOR FOR SELECT ID, Name FROM Employees;  
OPEN EmployeeCursor;  
FETCH NEXT FROM EmployeeCursor INTO @ID, @Name;  
-- I used cursors in legacy systems for row-level operations that lacked set-based solutions.
```

### **33. Explain Function vs. Stored Procedure in SQL Server.**  
- Functions return a value (scalar or table), while procedures execute code without necessarily returning a value.  
- Functions are used in `SELECT` and other expressions; procedures cannot be used like this.  
- Functions cannot have side effects like modifying data; procedures can.  
- Example:  
```sql
CREATE FUNCTION GetEmployeeSalary(@ID INT) RETURNS INT  
AS  
BEGIN  
    RETURN (SELECT Salary FROM Employees WHERE ID = @ID);  
END;  
-- I used functions for calculations and procedures for complex business logic.
```

### **34. What are Row Constructors in SQL Server?**  
- Row constructors allow multiple rows of values to be inserted in a single `INSERT` statement.  
- Useful for quickly inserting data without repeating the column list.  
- Supported from SQL Server 2008 onwards.  
- Example:  
```sql
INSERT INTO Employees (ID, Name, Salary) VALUES  
(1, 'John', 50000),  
(2, 'Jane', 60000);  
-- I used row constructors to initialize lookup tables with static values.
```

### **35. What is a Linked Server in SQL Server?**  
- A linked server connects SQL Server to external databases or data sources.  
- Enables cross-database queries without data migration.  
- Configured using `sp_addlinkedserver`.  
- Example:  
```sql
SELECT * FROM [LinkedServerName].[DatabaseName].[Schema].[TableName];  
-- I used linked servers to integrate data from Oracle and SQL Server systems for a BI project.
```

### **36. What is a Filegroup in SQL Server?**  
- A filegroup is a logical storage unit for grouping data files.  
- It helps manage and allocate storage across multiple physical disks.  
- Primary filegroups store metadata, while secondary ones store user data.  
- Example:  
```sql
CREATE DATABASE MyDB  
ON PRIMARY  
(NAME = MyDB_Data, FILENAME = 'C:\MyDBData.mdf')  
LOG ON  
(NAME = MyDB_Log, FILENAME = 'C:\MyDBLog.ldf');  
-- I used filegroups to optimize performance by distributing data across disks.
```

### **37. Is it possible to import data directly from T-SQL commands without using SQL Server Integration Services? If so, what are the commands?**  
- Yes, you can use commands like `BULK INSERT`, `OPENROWSET`, or linked server queries.  
- `BULK INSERT` is efficient for loading large data files.  
- `OPENROWSET` allows querying external files.  
- Example:  
```sql
BULK INSERT Employees  
FROM 'C:\Data\Employees.csv'  
WITH (FIRSTROW = 2, FIELDTERMINATOR = ',', ROWTERMINATOR = '\n');  
-- I used BULK INSERT to load large CSV datasets into staging tables.
```

### **38. What is the difference between PARTITION BY and GROUP BY in SQL?**  
- `GROUP BY` aggregates rows into groups, reducing the number of rows in the result.  
- `PARTITION BY` provides row-wise aggregation without reducing rows, often used with window functions.  
- Both organize data but serve different purposes in aggregation.  
- Example:  
```sql
SELECT Name, Salary, RANK() OVER (PARTITION BY Department ORDER BY Salary DESC) AS Rank  
FROM Employees;  
-- I used PARTITION BY for generating rank-based reports without losing details.
```

### **39. What do Clustered and Non-Clustered indexes actually mean?**  
- A clustered index sorts and stores data rows in the table based on the index key.  
- A non-clustered index creates a separate structure pointing to table rows.  
- Each table can have one clustered index but multiple non-clustered indexes.  
- Example:  
```sql
CREATE CLUSTERED INDEX idx_employee_id ON Employees(ID);  
CREATE NONCLUSTERED INDEX idx_employee_name ON Employees(Name);  
-- I used a clustered index on primary keys and non-clustered for search columns.
```

### **40. Name some types of Triggers in SQL Server.**  
- **DML Triggers**: Execute on `INSERT`, `UPDATE`, or `DELETE`.  
- **DDL Triggers**: Fire on schema changes like `CREATE` or `ALTER`.  
- **Logon Triggers**: Execute during user logins.  
- Example:  
```sql
CREATE TRIGGER trg_employee_update  
ON Employees  
AFTER UPDATE  
AS  
    PRINT 'Employee record updated';  
-- I used triggers to log changes in sensitive tables.
```

### **41. What is the difference between EXEC vs sp_executesql in SQL Server?**  
- `EXEC` executes a SQL string but does not support parameters.  
- `sp_executesql` supports parameterized queries, reducing SQL injection risks.  
- `sp_executesql` allows query plan reuse, improving performance.  
- Example:  
```sql
DECLARE @SQL NVARCHAR(MAX) = 'SELECT * FROM Employees WHERE ID = @ID';  
DECLARE @ID INT = 1;  
EXEC sp_executesql @SQL, N'@ID INT', @ID;  
-- I used sp_executesql to dynamically query user-specific data securely.
```

### **42. What is the use of GO in Transact SQL?**  
- `GO` indicates the end of a batch of T-SQL statements.  
- It is not a SQL command but a batch separator in tools like SSMS.  
- Statements before `GO` are executed together, helping structure scripts.  
- Example:  
```sql
PRINT 'Batch 1';  
GO  
PRINT 'Batch 2';  
-- I used GO to organize long scripts for database deployment.
```

### **43. Is it correct/best practice to have the TRY/CATCH block inside the transaction or should the transaction be inside the TRY block?**  
- Best practice is to have the transaction inside the TRY block.  
- This ensures proper rollback in case of errors.  
- Avoid committing or rolling back outside of TRY/CATCH.  
- Example:  
```sql
BEGIN TRY  
    BEGIN TRANSACTION  
    INSERT INTO Orders (ID, OrderDate) VALUES (1, NULL);  
    COMMIT TRANSACTION;  
END TRY  
BEGIN CATCH  
    ROLLBACK TRANSACTION;  
    PRINT ERROR_MESSAGE();  
END CATCH;  
-- I used this approach for ensuring data consistency in critical operations.
```

### **44. What are the best practices for using a GUID as a primary key, specifically regarding performance?**  
- Use GUIDs as non-clustered indexes to avoid fragmentation.  
- Prefer sequential GUIDs (`NEWSEQUENTIALID`) for clustered indexes.  
- Monitor performance impact with large datasets.  
- Example:  
```sql
CREATE TABLE Products (ID UNIQUEIDENTIFIER PRIMARY KEY DEFAULT NEWID(), Name NVARCHAR(50));  
-- I used GUIDs as primary keys in distributed systems requiring global uniqueness.
```

### **45. What is the native system stored procedure to issue a command against all databases?**  
- Use `sp_MSforeachdb` to run a command across all databases.  
- It simplifies tasks like collecting information or applying updates.  
- Example:  
```sql
EXEC sp_MSforeachdb 'USE [?]; SELECT DB_NAME() AS DatabaseName, COUNT(*) FROM sys.tables';  
-- I used this procedure to audit table counts across multiple databases.
```

### **46. Why should you never use GUIDs as part of a clustered index?**  
- GUIDs are non-sequential, leading to high fragmentation in clustered indexes.  
- This affects insert performance and storage efficiency.  
- Use sequential GUIDs or surrogate keys instead.  
- Example:  
```sql
CREATE TABLE Products (ID UNIQUEIDENTIFIER DEFAULT NEWID(), Name NVARCHAR(50));  
CREATE NONCLUSTERED INDEX idx_product_id ON Products(ID);  
-- I avoided clustered GUID indexes after observing fragmentation issues in large datasets.
```

### **47. From a T-SQL perspective, how would you prevent T-SQL code from running on a production SQL Server?**  
- Use a check for the server name or environment variable at the beginning of the script.  
- Abort execution if the server is production.  
- Example:  
```sql
IF @@SERVERNAME = 'ProdServer'  
BEGIN  
    PRINT 'This script cannot run on production!';  
    RETURN;  
END;  
-- I used this safeguard to prevent accidental deployments on production environments.
```



### **48. How can you capture the length of a column when it is a Text, NText, or Image data type?**  
- Use the `DATALENGTH()` function to return the length in bytes of these data types.  
- `LEN()` does not work with `TEXT`, `NTEXT`, or `IMAGE`.  
- Consider converting `TEXT`/`NTEXT` to `VARCHAR` or `NVARCHAR` before using `LEN()` for string length.  
- Example:  
```sql
SELECT DATALENGTH(ColumnName) FROM MyTable;  
-- I used DATALENGTH() to analyze large text data in logging systems.
```

### **49. Provide an example of Left Outer Join with Exclusions.**  
- A `LEFT OUTER JOIN` returns all rows from the left table and matching rows from the right table; non-matching rows on the right will have `NULL`.  
- To exclude non-matching rows, use `WHERE` clause filtering.  
- Example:  
```sql
SELECT A.Name, B.Address  
FROM Customers A  
LEFT OUTER JOIN Orders B ON A.CustomerID = B.CustomerID  
WHERE B.OrderID IS NULL;  
-- I used this query to find customers who have never placed an order.
```

### **50. How do I UPDATE from a SELECT in SQL Server?**  
- You can perform an `UPDATE` based on the result of a `SELECT` query using a `JOIN` or `WHERE` clause.  
- This is useful for updating rows based on data from another table or query result.  
- Example:  
```sql
UPDATE A  
SET A.Salary = B.NewSalary  
FROM Employees A  
JOIN SalaryUpdates B ON A.EmployeeID = B.EmployeeID;  
-- I used this technique for updating salaries based on a bulk upload of new salary data.
```

### **51. How do TRUNCATE and DELETE operations affect Identity columns?**  
- `TRUNCATE` resets the identity column to its seed value.  
- `DELETE` does not affect the identity column and continues the count from the last inserted value.  
- Be cautious when using `TRUNCATE` as it may affect auto-increment behavior.  
- Example:  
```sql
TRUNCATE TABLE Products;  
-- I used TRUNCATE when I needed to clear tables and reset identity values in staging environments.
```

### **52. How to insert the results of a stored procedure into a temporary table?**  
- You can insert the result of a stored procedure into a temporary table using `INSERT INTO #TempTable`.  
- Ensure the stored procedure returns a result set.  
- Example:  
```sql
CREATE TABLE #TempResults (ID INT, Name NVARCHAR(50));  
INSERT INTO #TempResults  
EXEC GetEmployeeDetails;  
-- I used this approach to capture procedure results for further analysis without re-running the procedure.
```

---
