**1. How do you implement a try-catch block in SQL Server for error handling?**  
- A `TRY...CATCH` block in SQL Server captures errors during the execution of SQL code.  
- The `TRY` block contains the code that might generate an error, while the `CATCH` block handles the error.  
- In the `CATCH` block, you can retrieve error details using functions like `ERROR_MESSAGE()` and `ERROR_NUMBER()`.  
- You can use error handling to log errors, rollback transactions, or provide custom error messages.  
- Example: I implemented error handling to log transactional failures in an e-commerce platform.  
```sql
BEGIN TRY  
    BEGIN TRANSACTION  
    UPDATE Products SET Stock = Stock - 1 WHERE ProductID = 1;  
    -- Simulate error  
    INSERT INTO Orders(ProductID, Quantity) VALUES (1, 'INVALID_DATA');  
    COMMIT TRANSACTION  
END TRY  
BEGIN CATCH  
    ROLLBACK TRANSACTION  
    PRINT 'Error occurred: ' + ERROR_MESSAGE();  
END CATCH  
```

**2. What are correlated subqueries, and when would you use them in SQL?**  
- A correlated subquery is a subquery that depends on the outer query for its values.  
- It is executed once for each row processed by the outer query.  
- They are commonly used for row-by-row comparisons or calculations.  
- Correlated subqueries can be inefficient for large datasets due to repeated execution.  
- Example: I used correlated subqueries to calculate rank in an employee salary comparison system.  
```sql
SELECT e1.EmployeeID, e1.Salary,  
       (SELECT COUNT(*) FROM Employees e2 WHERE e2.Salary > e1.Salary) AS Rank  
FROM Employees e1;  
```

**3. How do you configure isolation levels in SQL transactions, and why are they important?**  
- Isolation levels determine how transactions interact with each other in SQL.  
- Common levels are `READ UNCOMMITTED`, `READ COMMITTED`, `REPEATABLE READ`, and `SERIALIZABLE`.  
- Lower isolation levels improve performance but can cause issues like dirty reads or phantom reads.  
- Higher isolation levels ensure data consistency but may increase locking and reduce concurrency.  
- Example: I configured `READ COMMITTED` to balance consistency and performance in a banking application.  
```sql
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;  
BEGIN TRANSACTION;  
UPDATE Accounts SET Balance = Balance - 100 WHERE AccountID = 1;  
UPDATE Accounts SET Balance = Balance + 100 WHERE AccountID = 2;  
COMMIT TRANSACTION;  
```

**4. What is a dead letter queue in SQL-based workflows, and how do you handle it?**  
- A dead letter queue stores messages that fail to be processed.  
- It is used to isolate and troubleshoot problematic transactions.  
- Messages can be analyzed for root cause, such as format errors or system issues.  
- Regular monitoring and automated retries can improve system resilience.  
- Example: I configured a dead letter queue in a Service Bus to handle unprocessable orders.  
```sql
-- Example for handling dead messages  
SELECT * FROM DeadLetterQueue WHERE ErrorCode IS NOT NULL;  
```

**5. How do you optimize queries involving large joins in SQL Server?**  
- Ensure appropriate indexes on join columns for efficient lookup.  
- Reduce the dataset size with filters or pre-aggregations before joining.  
- Avoid Cartesian joins by using proper `ON` conditions.  
- Use query hints like `OPTION (HASH JOIN)` for specific join strategies.  
- Example: I optimized a report generation query with large joins using indexing.  
```sql
CREATE INDEX idx_Orders_CustomerID ON Orders(CustomerID);  
SELECT o.OrderID, c.Name  
FROM Orders o  
JOIN Customers c ON o.CustomerID = c.CustomerID;  
```  

**6. What are the differences between temp tables and table variables, and when would you choose one over the other?**  
- Temp tables (`#TempTable`) are created in the `tempdb` database and can have indexes.  
- Table variables (`@TableVariable`) are stored in memory and generally have a smaller scope.  
- Temp tables can be shared between procedures if they exist in the same session, while table variables cannot.  
- Temp tables are better for large datasets and complex operations, while table variables work well for smaller data and simple tasks.  
- Example: I used temp tables for large joins and aggregations in reporting, while table variables were used for lightweight data passing.  
```sql
-- Temp table example  
CREATE TABLE #TempTable (ID INT, Name NVARCHAR(50));  
INSERT INTO #TempTable VALUES (1, 'John'), (2, 'Jane');  
SELECT * FROM #TempTable;  
```

**7. What is the role of primary and secondary replicas in SQL Server Always On Availability Groups?**  
- The primary replica handles read and write operations and manages the data synchronization.  
- Secondary replicas provide high availability and can be used for read-only queries.  
- Replication modes include synchronous (guaranteed consistency) and asynchronous (faster but eventual consistency).  
- Automatic failover occurs between primary and secondary replicas during downtime in synchronous mode.  
- Example: I configured Always On for high availability in a financial system to ensure uninterrupted service.  
```sql
-- Query on a read-only secondary replica  
SELECT * FROM Sales WITH (NOLOCK);  
```

**8. How do you use Common Table Expressions (CTEs) in SQL to simplify complex queries?**  
- A CTE is a temporary result set defined within the execution scope of a single SQL statement.  
- It simplifies complex queries by breaking them into smaller, manageable parts.  
- CTEs can be recursive, making them useful for hierarchical data.  
- They improve readability and can replace subqueries or derived tables.  
- Example: I used a recursive CTE to query hierarchical employee data.  
```sql
WITH EmployeeHierarchy AS (  
    SELECT EmployeeID, ManagerID, Name  
    FROM Employees  
    WHERE ManagerID IS NULL  
    UNION ALL  
    SELECT e.EmployeeID, e.ManagerID, e.Name  
    FROM Employees e  
    INNER JOIN EmployeeHierarchy eh ON e.ManagerID = eh.EmployeeID  
)  
SELECT * FROM EmployeeHierarchy;  
```

**9. Explain the purpose and benefits of indexed views in SQL Server, and how do they improve query performance?**  
- Indexed views store query results physically, improving performance for repetitive queries.  
- They are especially useful for pre-aggregated data or frequently accessed joins.  
- Unlike standard views, they require schema binding and specific design rules.  
- Query optimizer can use indexed views automatically if their indexed columns are included in the query.  
- Example: I used indexed views to speed up dashboard reporting in a retail application.  
```sql
CREATE VIEW SalesSummary WITH SCHEMABINDING AS  
SELECT ProductID, SUM(Quantity) AS TotalQuantity  
FROM Sales  
GROUP BY ProductID;  
CREATE UNIQUE CLUSTERED INDEX idx_SalesSummary ON SalesSummary(ProductID);  
```

**10. How do you optimize SQL queries for performance in high-traffic systems?**  
- Use appropriate indexes to minimize table scans.  
- Optimize query plans with `EXPLAIN` or `Execution Plan`.  
- Reduce query complexity with pre-aggregations or intermediate tables.  
- Cache results for frequently accessed data using in-memory solutions.  
- Example: I reduced query latency by adding non-clustered indexes in a ticket booking system.  
```sql
CREATE NONCLUSTERED INDEX idx_Booking_Date ON Bookings(BookingDate);  
```

**11. What are the differences between clustered and non-clustered indexes?**  
- Clustered indexes sort and store data rows in the table based on the key.  
- Non-clustered indexes store pointers to the actual data rows.  
- A table can have only one clustered index but multiple non-clustered indexes.  
- Clustered indexes are better for range queries, while non-clustered ones excel in lookups.  
- Example: I used clustered indexes for primary keys and non-clustered for search columns.  
```sql
CREATE CLUSTERED INDEX idx_OrderID ON Orders(OrderID);  
CREATE NONCLUSTERED INDEX idx_CustomerID ON Orders(CustomerID);  
```

**12. How do you create and use stored procedures with optional parameters?**  
- Optional parameters have default values in the procedure definition.  
- If a value is not provided during execution, the default value is used.  
- Simplifies query customization by reusing the same procedure.  
- Reduces the need for multiple procedure versions.  
- Example: I created a stored procedure for filtering products by category or price range.  
```sql
CREATE PROCEDURE GetProducts  
    @Category NVARCHAR(50) = NULL,  
    @Price DECIMAL(10, 2) = NULL  
AS  
BEGIN  
    SELECT * FROM Products  
    WHERE (@Category IS NULL OR Category = @Category)  
      AND (@Price IS NULL OR Price <= @Price);  
END;  
```

**13. What are isolation levels in SQL Server, and how do they affect data consistency?**  
- Isolation levels manage the visibility of data changes during a transaction.  
- Levels include `READ UNCOMMITTED`, `READ COMMITTED`, `REPEATABLE READ`, and `SERIALIZABLE`.  
- Lower levels allow more concurrency but risk data anomalies like dirty reads.  
- Higher levels ensure consistency but may lock resources longer.  
- Example: I used `REPEATABLE READ` to prevent phantom reads in inventory management.  
```sql
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;  
BEGIN TRANSACTION;  
SELECT * FROM Inventory WHERE ProductID = 1;  
UPDATE Inventory SET Quantity = Quantity - 10 WHERE ProductID = 1;  
COMMIT TRANSACTION;  
```

**14. What are the different types of joins in SQL, and when would you use each?**  
- `INNER JOIN` retrieves rows with matching values in both tables.  
- `LEFT JOIN` retrieves all rows from the left table and matching rows from the right.  
- `RIGHT JOIN` retrieves all rows from the right table and matching rows from the left.  
- `FULL OUTER JOIN` retrieves all rows when there’s a match in either table.  
- Example: I used `LEFT JOIN` to fetch customer orders even when no orders exist.  
```sql
SELECT c.CustomerName, o.OrderID  
FROM Customers c  
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID;  
```

**15. How do you handle deadlocks in SQL Server?**  
- Identify and resolve conflicting transactions using SQL Profiler or deadlock graphs.  
- Minimize locking with shorter transactions and proper indexing.  
- Use `SET DEADLOCK_PRIORITY` to control which transaction is terminated.  
- Implement retry logic in the application layer for resiliency.  
- Example: I analyzed and resolved deadlocks in a payment system by optimizing resource access order.  
```sql
SET DEADLOCK_PRIORITY LOW;  
BEGIN TRANSACTION;  
UPDATE Accounts SET Balance = Balance - 100 WHERE AccountID = 1;  
UPDATE Accounts SET Balance = Balance + 100 WHERE AccountID = 2;  
COMMIT TRANSACTION;  
```

**16. What is the purpose of database normalization, and what are its normal forms?**  
- Normalization reduces data redundancy and ensures data integrity in a relational database.  
- It organizes data into smaller, related tables with well-defined relationships.  
- Normal forms include 1NF (Atomicity), 2NF (No Partial Dependencies), 3NF (No Transitive Dependencies), BCNF, and beyond.  
- Higher normal forms improve data consistency but may reduce query performance due to joins.  
- Example: I normalized a sales database to 3NF, which eliminated redundancy in product and order information.  
```sql
-- Example: Splitting Product and Supplier data  
CREATE TABLE Products (ProductID INT PRIMARY KEY, ProductName NVARCHAR(50), SupplierID INT);  
CREATE TABLE Suppliers (SupplierID INT PRIMARY KEY, SupplierName NVARCHAR(50));  
```

**17. How do you monitor and optimize SQL Server performance using execution plans?**  
- Execution plans provide a visual representation of the query execution process.  
- They help identify bottlenecks such as table scans or missing indexes.  
- Common optimization strategies include creating indexes, rewriting queries, and reducing complexity.  
- Tools like SQL Server Management Studio (SSMS) provide graphical execution plan analysis.  
- Example: I optimized slow queries in a reporting system by analyzing execution plans and adding missing indexes.  
```sql
-- Display execution plan  
SET SHOWPLAN_XML ON;  
SELECT * FROM Orders WHERE OrderDate > '2024-01-01';  
SET SHOWPLAN_XML OFF;  
```

**18. How do you secure sensitive data in SQL Server using encryption?**  
- Use Transparent Data Encryption (TDE) to encrypt data at rest.  
- Column-level encryption protects specific sensitive columns like SSNs or credit card numbers.  
- Always encrypt connections to SQL Server using SSL/TLS.  
- Use SQL Server’s Always Encrypted feature for end-to-end data protection.  
- Example: I implemented TDE for customer data in a compliance-sensitive application.  
```sql
-- Enabling TDE  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_256 ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
ALTER DATABASE MyDatabase SET ENCRYPTION ON;  
```

**19. What is the difference between INNER JOIN, LEFT JOIN, RIGHT JOIN, and FULL OUTER JOIN?**  
- `INNER JOIN`: Returns rows with matching values in both tables.  
- `LEFT JOIN`: Returns all rows from the left table and matching rows from the right.  
- `RIGHT JOIN`: Returns all rows from the right table and matching rows from the left.  
- `FULL OUTER JOIN`: Returns all rows from both tables, with NULLs where no match exists.  
- Example: I used `FULL OUTER JOIN` to compare inventory data from two systems for reconciliation.  
```sql
SELECT a.ProductID, a.Quantity AS SystemA, b.Quantity AS SystemB  
FROM InventoryA a  
FULL OUTER JOIN InventoryB b ON a.ProductID = b.ProductID;  
```

**20. How do you handle error logging and exception handling in SQL Server stored procedures?**  
- Use `TRY...CATCH` blocks for error handling within stored procedures.  
- Log errors into an error table for later analysis using `INSERT INTO`.  
- Retrieve error details using functions like `ERROR_MESSAGE()` and `ERROR_LINE()`.  
- Implement a centralized error handling mechanism across procedures.  
- Example: I logged errors in an audit table to track failed transactions in a billing system.  
```sql
BEGIN TRY  
    -- Your SQL logic  
END TRY  
BEGIN CATCH  
    INSERT INTO ErrorLog(ErrorMessage, ErrorLine)  
    VALUES (ERROR_MESSAGE(), ERROR_LINE());  
END CATCH;  
```

**21. What are triggers in SQL, and how do they differ from stored procedures?**  
- Triggers are automatically executed in response to specific events like `INSERT`, `UPDATE`, or `DELETE`.  
- Stored procedures are executed explicitly by users or applications.  
- Triggers enforce business rules or data integrity, while procedures provide reusable logic.  
- Triggers run within the context of the event and cannot be directly invoked.  
- Example: I used a trigger to update inventory levels automatically after a sale.  
```sql
CREATE TRIGGER UpdateInventory AFTER INSERT ON Sales  
FOR EACH ROW  
BEGIN  
    UPDATE Inventory SET Quantity = Quantity - NEW.Quantity  
    WHERE ProductID = NEW.ProductID;  
END;  
```

**22. How do you implement table partitioning in SQL Server for large datasets?**  
- Table partitioning divides a table into smaller, manageable pieces for improved performance.  
- Partitions are created based on a range of values, typically on a date or ID column.  
- Use partition functions to define boundaries and partition schemes to assign storage.  
- Improves query performance and reduces maintenance effort on large tables.  
- Example: I implemented partitioning on a log table to improve query speed for recent logs.  
```sql
CREATE PARTITION FUNCTION LogPartitionFunction(DATE)  
AS RANGE RIGHT FOR VALUES ('2024-01-01', '2024-02-01', '2024-03-01');  
CREATE PARTITION SCHEME LogPartitionScheme  
AS PARTITION LogPartitionFunction ALL TO ([PRIMARY]);  
```

**23. How do you perform bulk insert operations efficiently in SQL Server?**  
- Use the `BULK INSERT` statement for importing large volumes of data quickly.  
- Optimize with batch sizes and disable indexes during insertion.  
- Use the `TABLOCK` hint for minimal logging in bulk-logged or simple recovery models.  
- Pre-sort data to match the table’s clustered index for improved performance.  
- Example: I used `BULK INSERT` to migrate historical data into a warehouse system.  
```sql
BULK INSERT Sales  
FROM 'C:\Data\SalesData.csv'  
WITH (FIELDTERMINATOR = ',', ROWTERMINATOR = '\n', FIRSTROW = 2);  
```

**24. What is SQL Profiler, and how do you use it to troubleshoot performance issues?**  
- SQL Profiler is a tool for monitoring and capturing SQL Server activity.  
- It helps identify slow queries, blocking, and resource-intensive operations.  
- Use it to capture traces for analysis and tune queries accordingly.  
- Be cautious with live production servers to avoid overhead.  
- Example: I used SQL Profiler to diagnose slow database performance in an ERP system.  
```sql
-- No code for Profiler; open and configure in SQL Server Management Studio (SSMS).  
```

**25. How do you design a database schema for a multi-tenant SaaS application?**  
- Use separate schemas or databases for strict isolation.  
- Use shared tables with tenant ID columns for resource efficiency.  
- Normalize common data and denormalize tenant-specific data for performance.  
- Implement row-level security to enforce tenant isolation.  
- Example: I designed a multi-tenant application where tenant-specific data was identified by a TenantID column.  
```sql
CREATE TABLE Orders (OrderID INT, TenantID INT, ProductID INT, Quantity INT);  
```

**26. What are foreign keys and primary keys, and how are they enforced in SQL Server?**  
- A primary key uniquely identifies each row in a table.  
- A foreign key establishes a relationship between two tables.  
- Primary keys enforce uniqueness, while foreign keys enforce referential integrity.  
- Use `ON DELETE` or `ON UPDATE` options for cascading changes.  
- Example: I used foreign keys to link orders to customers in an e-commerce database.  
```sql
CREATE TABLE Customers (CustomerID INT PRIMARY KEY, Name NVARCHAR(50));  
CREATE TABLE Orders (OrderID INT PRIMARY KEY, CustomerID INT FOREIGN KEY REFERENCES Customers(CustomerID));  
```

**27. How do you use dynamic SQL, and what are the security considerations involved?**  
- Dynamic SQL allows the execution of SQL strings built at runtime.  
- Useful for flexible query generation and handling variable conditions.  
- Avoid SQL injection by using parameterized queries or `sp_executesql`.  
- Validate user inputs rigorously before constructing dynamic SQL.  
- Example: I used dynamic SQL to generate reports dynamically based on user-selected columns.  
```sql
DECLARE @sql NVARCHAR(MAX);  
SET @sql = 'SELECT ' + @ColumnName + ' FROM Sales';  
EXEC sp_executesql @sql;  
```

**28. What are the differences between OLTP and OLAP databases?**  
- OLTP (Online Transaction Processing) is optimized for transactional systems, with frequent writes.  
- OLAP (Online Analytical Processing) is designed for querying and analysis, with read-intensive operations.  
- OLTP databases have normalized schemas, while OLAP uses denormalized schemas like star or snowflake.  
- OLTP supports real-time operations; OLAP supports historical data analysis.  
- Example: I built an OLTP database for retail transactions and an OLAP system for sales reporting.  

**29. How do you configure SQL Server replication for data synchronization across regions?**  
- Configure transactional replication for near real-time synchronization.  
- Use merge replication for bi-directional synchronization across regions.  
- Snapshot replication sends a full copy of the data periodically.  
- Consider network latency and conflict resolution strategies for global setups.  
- Example: I used transactional replication to sync regional sales databases with a central warehouse.  

**30. What is a materialized view, and how does it differ from a standard view?**  
- A materialized view stores query results physically, unlike a standard view, which is virtual.  
- It improves performance for repetitive and complex queries.  
- Needs manual or scheduled refresh to update data.  


- Example: I used materialized views in a BI system for pre-aggregating sales data.  
```sql
CREATE MATERIALIZED VIEW SalesSummary AS  
SELECT ProductID, SUM(Quantity) AS TotalQuantity FROM Sales GROUP BY ProductID;  
```

**31. How do you back up and restore databases in SQL Server?**  
- Use `BACKUP DATABASE` for full, differential, or transaction log backups.  
- Full backups create a complete copy of the database.  
- Differential backups store changes since the last full backup.  
- Transaction log backups capture changes since the last log backup for point-in-time recovery.  
- Example: I scheduled regular full backups and differential backups for a production database.  
```sql
-- Backup a database  
BACKUP DATABASE MyDatabase TO DISK = 'C:\Backups\MyDatabase.bak';  
-- Restore a database  
RESTORE DATABASE MyDatabase FROM DISK = 'C:\Backups\MyDatabase.bak';  
```

**32. What are the benefits of using partitioned indexes in large databases?**  
- Partitioned indexes improve query performance by targeting specific partitions.  
- They reduce index maintenance overhead for large datasets.  
- Useful for range queries, such as those involving dates.  
- Can be aligned with table partitions for consistency.  
- Example: I created partitioned indexes on a log table to improve search performance for recent entries.  
```sql
CREATE PARTITION FUNCTION MyPartitionFunction (INT)  
AS RANGE LEFT FOR VALUES (100, 200, 300);  
CREATE PARTITION SCHEME MyPartitionScheme  
AS PARTITION MyPartitionFunction ALL TO ([PRIMARY]);  
CREATE INDEX IX_Partitioned ON MyTable (ColumnName)  
ON MyPartitionScheme (ColumnName);  
```

**33. How do you use window functions in SQL for analytical queries?**  
- Window functions operate over a defined set of rows (the window).  
- Common functions include `ROW_NUMBER()`, `RANK()`, `NTILE()`, and aggregate functions with `OVER()`.  
- They enable ranking, cumulative totals, and moving averages.  
- Do not group rows but calculate results for each row within a partition.  
- Example: I used `ROW_NUMBER()` to paginate results in a reporting application.  
```sql
SELECT ROW_NUMBER() OVER (ORDER BY OrderDate DESC) AS RowNum, OrderID, OrderDate  
FROM Orders;  
```

**34. How do you identify and resolve blocking queries in SQL Server?**  
- Use `sp_who2` or SQL Server Management Studio to identify blocked processes.  
- Analyze query execution plans to find slow or inefficient queries causing blocks.  
- Optimize indexes and query structure to reduce locking.  
- Use `SET TRANSACTION ISOLATION LEVEL` to minimize contention.  
- Example: I resolved blocking issues in a payroll system by optimizing queries and reducing lock duration.  
```sql
-- Check blocking queries  
EXEC sp_who2;  
```

**35. How do you implement database partitioning for scalability?**  
- Divide a large table into smaller, manageable partitions based on range, list, or hash.  
- Improve query performance by reducing the amount of scanned data.  
- Use partition functions and schemes to define boundaries and storage.  
- Supports efficient data archiving and maintenance.  
- Example: I partitioned a transaction table by year to improve query speed for recent data.  
```sql
CREATE PARTITION FUNCTION YearPartitionFunction (DATE)  
AS RANGE RIGHT FOR VALUES ('2023-01-01', '2024-01-01');  
CREATE PARTITION SCHEME YearPartitionScheme  
AS PARTITION YearPartitionFunction ALL TO ([PRIMARY]);  
```

**36. What is the MERGE statement, and how can it be used for upsert operations?**  
- The `MERGE` statement combines `INSERT`, `UPDATE`, and `DELETE` in a single operation.  
- Useful for synchronizing two tables or performing upserts.  
- Requires a source and target table with a join condition.  
- Can include multiple actions like updating matched rows or inserting unmatched rows.  
- Example: I used `MERGE` to update and insert sales data into a consolidated table.  
```sql
MERGE INTO TargetTable AS Target  
USING SourceTable AS Source  
ON Target.ID = Source.ID  
WHEN MATCHED THEN UPDATE SET Target.Name = Source.Name  
WHEN NOT MATCHED THEN INSERT (ID, Name) VALUES (Source.ID, Source.Name);  
```

**37. How do you implement database sharding, and what are the key considerations for partitioning data?**  
- Sharding splits data across multiple databases or servers to distribute load.  
- Each shard contains a subset of data, often based on a shard key like customer ID.  
- Requires careful selection of shard keys to avoid uneven distribution.  
- Consider strategies for shard management, data replication, and cross-shard queries.  
- Example: I implemented sharding for a multi-region e-commerce application to reduce latency.  

**38. Explain the concept of a materialized view and how it differs from a regular view.**  
- A materialized view stores query results physically, unlike a regular view, which is virtual.  
- Improves performance by precomputing and storing complex query results.  
- Requires manual or scheduled refresh to keep data up-to-date.  
- Regular views always reflect the latest data but can be slower for complex queries.  
- Example: I used materialized views in a data warehouse to speed up reporting.  
```sql
CREATE MATERIALIZED VIEW SalesSummary AS  
SELECT ProductID, SUM(SalesAmount) AS TotalSales  
FROM Sales  
GROUP BY ProductID;  
```

**39. How do you handle deadlocks in SQL Server, and what strategies help prevent them?**  
- Detect deadlocks using the SQL Server error log or tools like Extended Events.  
- Analyze deadlock graphs to identify conflicting resources.  
- Reduce lock contention with shorter transactions and optimized queries.  
- Use `NOLOCK` or row versioning for read operations where possible.  
- Example: I resolved deadlocks in a ticketing system by optimizing locking mechanisms.  
```sql
-- Example deadlock resolution query optimization  
SELECT * FROM Orders WITH (NOLOCK) WHERE OrderStatus = 'Pending';  
```

**40. What is the purpose of the FOR JSON clause in SQL Server, and how does it work?**  
- The `FOR JSON` clause formats query results as JSON for API or front-end consumption.  
- Supports `AUTO` and `PATH` modes for different levels of customization.  
- Simplifies integration with applications expecting JSON data.  
- Useful for exporting data to web services or modern applications.  
- Example: I used `FOR JSON` to deliver query results in JSON format for a mobile app API.  
```sql
SELECT OrderID, CustomerName  
FROM Orders  
FOR JSON AUTO;  
```

**41. How can you implement a recursive query without using a Common Table Expression (CTE)?**  
- Use procedural logic like loops or cursors in SQL Server stored procedures.  
- Alternatively, emulate recursion with temporary tables or self-joins.  
- Recursive CTEs are generally preferred for cleaner, more readable queries.  
- Example: Without a CTE, I used a loop to calculate hierarchical relationships in an employee table.  

**42. What are hash indexes, and how do they differ from B-tree indexes?**  
- Hash indexes map keys to hash values for quick equality searches.  
- B-tree indexes support range and sorted queries, while hash indexes do not.  
- Hash indexes are faster for exact lookups but less versatile.  
- Common in NoSQL databases but rare in traditional RDBMS like SQL Server.  
- Example: Used hash indexing in a NoSQL database for a high-traffic key-value store.  

**43. Explain the use of temporal tables in SQL Server for tracking historical data.**  
- Temporal tables automatically track changes to data with system-managed history tables.  
- Provide insights into data changes over time.  
- Useful for auditing, reporting, and restoring previous states.  
- Example: I implemented temporal tables to track changes in customer records for compliance.  
```sql
CREATE TABLE Customers  
(  
    CustomerID INT PRIMARY KEY,  
    Name NVARCHAR(50),  
    ValidFrom DATETIME2 GENERATED ALWAYS AS ROW START,  
    ValidTo DATETIME2 GENERATED ALWAYS AS ROW END,  
    PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)  
) WITH (SYSTEM_VERSIONING = ON);  
```

**44. How do you analyze and interpret an execution plan to optimize SQL queries?**  
- Examine operators like scans, seeks, and joins to identify inefficiencies.  
- Look for warnings like missing indexes or expensive sort operations.  
- Evaluate estimated vs. actual rows for discrepancies.  
- Optimize problematic operators with indexing or query rewrites.  
- Example: Used execution plans to diagnose and fix slow joins in a reporting query.  

**45. What is the difference between optimistic and pessimistic locking in SQL?**  
- Optimistic locking assumes minimal conflicts and checks for changes before committing.  
- Pessimistic locking locks resources to prevent conflicts during a transaction.  
- Optimistic locking is better for read-heavy systems with low contention.  
- Pessimistic locking is used in write-heavy or high-contention scenarios.  
- Example: Used optimistic locking with row versioning in a read-intensive application.  

Here are some advanced and critical SQL Server-related questions to help you further prepare for interviews:

**46. How do you design high-availability solutions in SQL Server?**  
- Use Always On Availability Groups for read/write availability across replicas.  
- Implement failover clustering to provide automatic recovery during server failures.  
- Use database mirroring for redundancy and disaster recovery.  
- Regularly back up and test the disaster recovery plan.  
- Example: Configured an Always On Availability Group to ensure high availability in a financial system.  

**47. How do you handle and optimize parameter sniffing in SQL Server?**  
- Use `OPTION (RECOMPILE)` to create query-specific execution plans.  
- Employ forced parameterization or optimize queries with specific parameter hints.  
- Test and implement plan guides for targeted queries.  
- Regularly update statistics to ensure the query optimizer makes informed decisions.  
- Example: Added `OPTION (OPTIMIZE FOR UNKNOWN)` to resolve performance issues caused by parameter sniffing.  
```sql
SELECT * FROM Orders WHERE OrderDate = @OrderDate  
OPTION (OPTIMIZE FOR UNKNOWN);  
```

**48. How do you implement database version control?**  
- Use tools like SQL Server Data Tools (SSDT) or Flyway for schema versioning.  
- Maintain scripts for schema changes in a source control system like Git.  
- Use migration-based or state-based approaches for deployments.  
- Automate version control integration into CI/CD pipelines.  
- Example: Implemented database versioning using Flyway for a multi-environment deployment.  

**49. What is query optimization and why is it important?**  
- Query optimization improves performance by reducing resource usage and response time.  
- Techniques include indexing, avoiding unnecessary columns, and optimizing joins.  
- Analyze execution plans and query statistics to find inefficiencies.  
- Use table partitions and indexed views for complex queries.  
- Example: Optimized queries in an analytics system by rewriting joins and creating covering indexes.  

**50. How do you implement row-level security (RLS) in SQL Server?**  
- Use RLS to control access to rows based on user identity or context.  
- Create a security policy using predicates in inline table-valued functions.  
- Apply `FILTER` and `BLOCK` predicates for data filtering and update control.  
- Example: Implemented RLS to restrict access to sales data by region in a multi-tenant application.  
```sql
CREATE FUNCTION SecurityPredicate(@RegionID INT)  
RETURNS TABLE  
AS  
RETURN SELECT 1 AS Access WHERE @RegionID = USER_REGION();  
CREATE SECURITY POLICY RegionSecurity  
ADD FILTER PREDICATE dbo.SecurityPredicate(RegionID)  
ON Sales;  
```

**51. How do you perform schema comparison and synchronization?**  
- Use SQL Server Data Tools (SSDT) or third-party tools like Redgate SQL Compare.  
- Generate scripts to sync differences between source and target schemas.  
- Include schema comparison in your deployment pipeline for automation.  
- Example: Used Redgate SQL Compare to sync test and production databases during release cycles.  

**52. What are the differences between database mirroring and log shipping?**  
- Database mirroring provides real-time synchronization between primary and secondary databases.  
- Log shipping transfers transaction logs periodically for disaster recovery.  
- Mirroring is suitable for high-availability scenarios, while log shipping is ideal for reporting or backup systems.  
- Example: Used log shipping for offsite backups in a disaster recovery strategy.  

**53. How do you use CROSS APPLY and OUTER APPLY in SQL Server?**  
- `CROSS APPLY` works like an inner join for functions or table expressions.  
- `OUTER APPLY` includes rows even when the function or expression returns null.  
- Useful for invoking functions on each row of a table.  
- Example: Used `CROSS APPLY` to invoke a table-valued function for dynamic filtering.  
```sql
SELECT Orders.OrderID, Details.Quantity  
FROM Orders  
CROSS APPLY dbo.GetOrderDetails(Orders.OrderID) AS Details;  
```

**54. How do you perform transactional replication in SQL Server?**  
- Use transactional replication to replicate changes from a publisher to subscribers in near real-time.  
- Configure a distribution database to manage replication processes.  
- Suitable for high-transaction systems needing data consistency across servers.  
- Example: Used transactional replication to synchronize data between a reporting and a production database.  

**55. What are Indexed Views and their limitations?**  
- Indexed views store data physically for improved performance.  
- Useful for complex queries or aggregations requiring frequent access.  
- Limitations include restrictions on usage of certain functions, joins, and schema binding requirements.  
- Example: Used indexed views to precompute metrics in a dashboard system.  

**56. How do you prevent SQL injection attacks?**  
- Use parameterized queries or stored procedures to separate logic from data.  
- Avoid dynamic SQL or validate input rigorously.  
- Implement database security features like roles and permissions.  
- Example: Rewrote a dynamic SQL query to use parameters, eliminating potential injection risks.  
```sql
-- Vulnerable Query  
EXEC ('SELECT * FROM Users WHERE Username = ''' + @username + '''');  
-- Secured Query  
SELECT * FROM Users WHERE Username = @username;  
```

**57. How do you optimize a database for write-heavy applications?**  
- Use table partitions to distribute write load.  
- Optimize indexes for minimal maintenance during insert/update operations.  
- Implement batching for bulk operations.  
- Example: Optimized a messaging app by reducing index maintenance during high write loads.  

**58. How do you debug stored procedures in SQL Server?**  
- Use SQL Server Management Studio (SSMS) to step through stored procedures.  
- Add print statements or use `RAISERROR` for runtime diagnostics.  
- Enable profiling or Extended Events to track procedure performance.  
- Example: Debugged a stored procedure with unexpected output using `RAISERROR` statements.  

**59. What is the difference between schema binding and non-schema binding views?**  
- Schema binding ties a view to the underlying table structure, preventing changes to dependent objects.  
- Non-schema binding allows modifications to underlying tables.  
- Schema binding is essential for creating indexed views.  
- Example: Used schema binding in an indexed view for performance optimization.  

**60. How do you handle archiving and purging of large datasets?**  
- Use table partitioning for efficient data movement between active and archive tables.  
- Employ scheduled jobs to move or delete older data.  
- Maintain indexes separately for active and archive tables.  
- Example: Implemented a partitioning strategy to purge old order records while retaining recent ones.  

**61. What are the differences between a primary key and a unique key?**  
- A primary key uniquely identifies each row in a table and cannot have NULL values.  
- A unique key also ensures unique values but can allow one NULL value.  
- There can be only one primary key per table, but multiple unique keys are allowed.  
- Example: Used a unique key to prevent duplicate email entries in a user table while allowing one NULL.  
```sql
CREATE TABLE Users (  
    UserID INT PRIMARY KEY,  
    Email NVARCHAR(255) UNIQUE  
);  
```

**62. What is the difference between DELETE and TRUNCATE in SQL?**  
- DELETE removes specific rows based on a condition and logs each deletion.  
- TRUNCATE removes all rows from a table but does not log individual deletions, making it faster.  
- DELETE can be used with WHERE, while TRUNCATE cannot.  
- Example: Used TRUNCATE to reset a staging table before re-importing data.  
```sql
TRUNCATE TABLE StagingData;  
```

**63. How do you retrieve the current date and time in SQL Server?**  
- Use `GETDATE()` to retrieve the current date and time.  
- `SYSDATETIME()` provides higher precision for fractional seconds.  
- Useful for auditing or setting default values in timestamp columns.  
- Example: Used `GETDATE()` to record timestamps for user login events.  
```sql
INSERT INTO UserLogins (UserID, LoginTime) VALUES (1, GETDATE());  
```

**64. What is a NULL value in SQL, and how is it different from a blank or zero?**  
- NULL represents missing or unknown data, whereas blank is an empty string, and zero is a numeric value.  
- NULL is not equal to any value, including itself; use `IS NULL` to check for it.  
- Example: Used NULL to indicate unprovided optional fields in a form submission table.  
```sql
SELECT * FROM Users WHERE LastName IS NULL;  
```

**65. What is the difference between HAVING and WHERE clauses?**  
- `WHERE` filters rows before grouping, while `HAVING` filters groups after aggregation.  
- Both can be used together in a query for more granular control.  
- Example: Used `HAVING` to find products with total sales greater than 100.  
```sql
SELECT ProductID, SUM(SalesAmount) AS TotalSales  
FROM Sales  
GROUP BY ProductID  
HAVING SUM(SalesAmount) > 100;  
```

**66. How do you retrieve the top N rows from a table?**  
- Use the `TOP` keyword to limit the number of rows returned.  
- Combine with `ORDER BY` to specify the selection order.  
- Example: Retrieved the top 5 highest-paid employees from an HR database.  
```sql
SELECT TOP 5 EmployeeID, Salary  
FROM Employees  
ORDER BY Salary DESC;  
```

**67. What is the purpose of the COALESCE function in SQL?**  
- COALESCE returns the first non-NULL value from a list of arguments.  
- It is useful for handling NULL values in expressions or defaulting values.  
- Example: Used COALESCE to replace NULL values with "Unknown" in a report.  
```sql
SELECT EmployeeID, COALESCE(Department, 'Unknown') AS Department  
FROM Employees;  
```

**68. How do you rename a table or column in SQL Server?**  
- Use `sp_rename` to rename tables or columns.  
- Syntax: `sp_rename 'OldName', 'NewName', 'OBJECT_TYPE'`.  
- Example: Renamed a column from `OldColumn` to `NewColumn` in a legacy database.  
```sql
EXEC sp_rename 'Employees.OldColumn', 'NewColumn', 'COLUMN';  
```

**69. What is a composite key in SQL, and when would you use it?**  
- A composite key is a primary key that consists of two or more columns.  
- It is used when no single column can uniquely identify a row.  
- Example: Defined a composite key for a junction table in a many-to-many relationship.  
```sql
CREATE TABLE CourseRegistrations (  
    StudentID INT,  
    CourseID INT,  
    PRIMARY KEY (StudentID, CourseID)  
);  
```

**70. How do you retrieve duplicate rows from a table?**  
- Use `GROUP BY` with `HAVING COUNT(*) > 1` to find duplicate entries.  
- Combine with `ROW_NUMBER()` to handle duplicates explicitly.  
- Example: Identified duplicate customer entries in a CRM system.  
```sql
SELECT Email, COUNT(*)  
FROM Customers  
GROUP BY Email  
HAVING COUNT(*) > 1;  
```

**71. What are default constraints in SQL Server?**  
- Default constraints assign a default value to a column if no value is provided during insertion.  
- Useful for ensuring columns have meaningful defaults without manual input.  
- Example: Set a default value of `GETDATE()` for a CreatedAt column.  
```sql
CREATE TABLE Orders (  
    OrderID INT PRIMARY KEY,  
    CreatedAt DATETIME DEFAULT GETDATE()  
);  
```

**72. How do you calculate the total, average, or count of rows in a table?**  
- Use aggregate functions like `SUM()`, `AVG()`, and `COUNT()`.  
- Combine with `GROUP BY` for segmented calculations.  
- Example: Calculated the total sales for each product in a sales report.  
```sql
SELECT ProductID, SUM(SalesAmount) AS TotalSales  
FROM Sales  
GROUP BY ProductID;  
```

**73. How do you remove duplicate rows from a table?**  
- Use `ROW_NUMBER()` with a `CTE` to identify duplicates and delete them.  
- Retain only the desired instance of each duplicate.  
- Example: Removed duplicates from a customer database based on email.  
```sql
WITH CTE AS (  
    SELECT *, ROW_NUMBER() OVER (PARTITION BY Email ORDER BY ID) AS RowNum  
    FROM Customers  
)  
DELETE FROM CTE WHERE RowNum > 1;  
```

**74. What is the difference between CHAR and VARCHAR in SQL Server?**  
- `CHAR` has a fixed length, while `VARCHAR` has a variable length.  
- `VARCHAR` is more efficient for strings of varying lengths.  
- Example: Used VARCHAR for a description column in a product table to save storage.  
```sql
CREATE TABLE Products (  
    ProductID INT PRIMARY KEY,  
    Description VARCHAR(255)  
);  
```

**75. How do you find the nth highest salary in a table?**  
- Use the `OFFSET-FETCH` clause or a subquery with `ROW_NUMBER()`.  
- Example: Retrieved the 3rd highest salary from an Employees table.  
```sql
SELECT Salary  
FROM (SELECT Salary, ROW_NUMBER() OVER (ORDER BY Salary DESC) AS RowNum  
      FROM Employees) AS Ranked  
WHERE RowNum = 3;  
``` 

**76. What is the difference between UNION and UNION ALL in SQL?**  
- UNION combines result sets and removes duplicates, while UNION ALL includes duplicates.  
- UNION incurs more processing time due to duplicate removal.  
- Example: Used UNION ALL to merge two tables without filtering duplicate records.  
```sql
SELECT FirstName, LastName FROM Employees  
UNION ALL  
SELECT FirstName, LastName FROM Contractors;  
```

**77. What is the purpose of the CASE statement in SQL?**  
- CASE is used for conditional logic within queries.  
- It allows dynamic values or conditional grouping in SELECT, WHERE, or ORDER BY clauses.  
- Example: Categorized employees into salary ranges using a CASE statement.  
```sql
SELECT EmployeeID,  
       CASE  
           WHEN Salary < 50000 THEN 'Low'  
           WHEN Salary BETWEEN 50000 AND 100000 THEN 'Medium'  
           ELSE 'High'  
       END AS SalaryRange  
FROM Employees;  
```

**78. How do you retrieve metadata about database objects in SQL Server?**  
- Use system views like `INFORMATION_SCHEMA.TABLES` or `sys.objects`.  
- `sp_help` or `sp_columns` can also provide detailed object metadata.  
- Example: Retrieved a list of all tables in the database.  
```sql
SELECT TABLE_NAME  
FROM INFORMATION_SCHEMA.TABLES  
WHERE TABLE_TYPE = 'BASE TABLE';  
```

**79. What are system functions in SQL Server?**  
- System functions perform operations like string manipulation (`LEN`, `SUBSTRING`), date handling (`GETDATE`, `DATEADD`), and mathematical calculations (`ROUND`, `ABS`).  
- They are built-in and require no external libraries.  
- Example: Used `LEN` and `SUBSTRING` to extract a substring from a long text.  
```sql
SELECT SUBSTRING(FullName, 1, LEN(FullName) / 2) AS FirstHalf  
FROM Employees;  
```

**80. How do you implement pagination in SQL Server?**  
- Use the `OFFSET` and `FETCH` clauses for paging results.  
- Combine with `ORDER BY` for consistent results.  
- Example: Retrieved the second page of 10 records from a customer list.  
```sql
SELECT *  
FROM Customers  
ORDER BY CustomerID  
OFFSET 10 ROWS FETCH NEXT 10 ROWS ONLY;  
```

**81. What is the difference between DDL and DML commands in SQL?**  
- DDL (Data Definition Language) commands define schema structures (CREATE, ALTER, DROP).  
- DML (Data Manipulation Language) commands manage data within tables (INSERT, UPDATE, DELETE).  
- Example: Used DDL to add a column and DML to populate it.  
```sql
ALTER TABLE Employees ADD Department NVARCHAR(50);  
UPDATE Employees SET Department = 'HR' WHERE EmployeeID = 1;  
```

**82. How do you handle NULL values in SQL aggregate functions?**  
- Most aggregate functions like `SUM()` and `AVG()` ignore NULL values.  
- Use `ISNULL` or `COALESCE` to replace NULLs with default values.  
- Example: Calculated the total sales, replacing NULL amounts with 0.  
```sql
SELECT SUM(ISNULL(SalesAmount, 0)) AS TotalSales  
FROM Sales;  
```

**83. How do you create an auto-incrementing column in SQL Server?**  
- Use the `IDENTITY` property on an integer column.  
- Specify the seed and increment values.  
- Example: Created an OrderID column that starts at 1 and increments by 1.  
```sql
CREATE TABLE Orders (  
    OrderID INT IDENTITY(1, 1),  
    OrderDate DATETIME  
);  
```

**84. What is the purpose of the WITH(NOLOCK) hint in SQL Server?**  
- The `WITH(NOLOCK)` hint allows queries to read uncommitted data, improving performance.  
- It may result in dirty reads if data changes during the query.  
- Example: Used `NOLOCK` in a reporting query to avoid locking issues during high traffic.  
```sql
SELECT * FROM Orders WITH(NOLOCK);  
```

**85. How do you export query results to a file in SQL Server?**  
- Use SQL Server Management Studio (SSMS) to save query results as a file.  
- Use `bcp` (Bulk Copy Program) to export results programmatically.  
- Example: Exported a product list to a CSV file for a marketing team.  
```bash
bcp "SELECT * FROM Products" queryout "Products.csv" -c -T -S ServerName  
```

**86. How do you identify and remove orphaned rows in a database?**  
- Use `LEFT JOIN` to find rows without matching foreign key references.  
- Use DELETE based on the result of this query.  
- Example: Removed orphaned order details without parent orders.  
```sql
DELETE FROM OrderDetails  
WHERE OrderID NOT IN (SELECT OrderID FROM Orders);  
```

**87. What is the difference between CROSS JOIN and INNER JOIN?**  
- CROSS JOIN produces a Cartesian product of two tables (every combination).  
- INNER JOIN returns rows with matching values in specified columns.  
- Example: Used CROSS JOIN to generate all combinations of colors and sizes.  
```sql
SELECT * FROM Colors CROSS JOIN Sizes;  
```

**88. What is the difference between a physical and a logical delete?**  
- A physical delete removes rows permanently from a table.  
- A logical delete marks rows as inactive, typically using a flag column.  
- Example: Used a logical delete for soft-deleting user accounts.  
```sql
UPDATE Users SET IsActive = 0 WHERE UserID = 101;  
```

**89. How do you enforce referential integrity in SQL Server?**  
- Use foreign key constraints to enforce relationships between tables.  
- Specify cascading actions for updates or deletions (`ON DELETE CASCADE`).  
- Example: Created a foreign key to link orders to customers.  
```sql
ALTER TABLE Orders ADD CONSTRAINT FK_CustomerID FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID);  
```

**90. What is a computed column in SQL Server?**  
- A computed column derives its value from other columns in the table.  
- It can be persisted for faster querying.  
- Example: Created a computed column to calculate total price from quantity and unit price.  
```sql
CREATE TABLE OrderDetails (  
    Quantity INT,  
    UnitPrice DECIMAL(10, 2),  
    TotalPrice AS (Quantity * UnitPrice) PERSISTED  
);  
```

**91. What is the difference between a subquery and a JOIN?**  
- A subquery is a query within another query and returns data used by the outer query.  
- A JOIN combines rows from multiple tables based on a related column.  
- Example: Used a subquery to get the latest order date for each customer.  
```sql
SELECT CustomerID, (SELECT MAX(OrderDate) FROM Orders WHERE Orders.CustomerID = Customers.CustomerID) AS LatestOrder  
FROM Customers;  
```

**92. What are indexed views in SQL Server, and when would you use them?**  
- Indexed views store the result of a query physically on disk for faster retrieval.  
- They are beneficial for improving performance of queries involving heavy computations.  
- Example: Created an indexed view for aggregating sales data by region.  
```sql
CREATE VIEW SalesByRegion WITH SCHEMABINDING AS  
SELECT Region, SUM(SalesAmount) AS TotalSales  
FROM Sales GROUP BY Region;  
CREATE UNIQUE CLUSTERED INDEX IX_SalesByRegion ON SalesByRegion(Region);  
```

**93. What are cascading actions in foreign key constraints?**  
- Cascading actions (`ON DELETE CASCADE`, `ON UPDATE CASCADE`) ensure that related rows are updated or deleted automatically.  
- Helps maintain referential integrity without manual intervention.  
- Example: Set cascading delete to remove order details when an order is deleted.  
```sql
ALTER TABLE OrderDetails  
ADD CONSTRAINT FK_OrderID FOREIGN KEY (OrderID) REFERENCES Orders(OrderID) ON DELETE CASCADE;  
```

**94. What is the difference between stored procedures and functions in SQL?**  
- Stored procedures perform tasks and can return multiple result sets, while functions return a single value or table.  
- Functions cannot modify database state, whereas stored procedures can.  
- Example: Created a function to calculate discounts and a procedure for bulk order processing.  
```sql
CREATE FUNCTION CalculateDiscount(@Price DECIMAL, @DiscountRate DECIMAL)  
RETURNS DECIMAL AS  
BEGIN  
    RETURN @Price * (1 - @DiscountRate);  
END;  
```

**95. What is the difference between a unique constraint and a unique index?**  
- A unique constraint ensures no duplicate values in a column or combination of columns.  
- A unique index physically enforces the uniqueness and improves query performance.  
- Example: Added a unique constraint to prevent duplicate emails in a user table.  
```sql
CREATE TABLE Users (  
    UserID INT PRIMARY KEY,  
    Email NVARCHAR(255) UNIQUE  
);  
```

**96. How do you implement table inheritance in SQL Server?**  
- Use a parent table for shared attributes and child tables for specific attributes.  
- Use foreign key relationships to link child tables to the parent.  
- Example: Implemented table inheritance for different types of accounts.  
```sql
CREATE TABLE Accounts (AccountID INT PRIMARY KEY, AccountType NVARCHAR(50));  
CREATE TABLE SavingsAccounts (AccountID INT PRIMARY KEY, InterestRate DECIMAL, FOREIGN KEY (AccountID) REFERENCES Accounts(AccountID));  
CREATE TABLE CheckingAccounts (AccountID INT PRIMARY KEY, OverdraftLimit DECIMAL, FOREIGN KEY (AccountID) REFERENCES Accounts(AccountID));  
```

**97. What is the difference between INNER and OUTER APPLY in SQL Server?**  
- INNER APPLY returns rows from a table-valued function that produce matches.  
- OUTER APPLY includes all rows from the outer query, with NULLs for unmatched rows.  
- Example: Used OUTER APPLY to retrieve recent transactions, including customers with no transactions.  
```sql
SELECT C.CustomerID, T.TransactionID  
FROM Customers C  
OUTER APPLY (SELECT TOP 1 TransactionID FROM Transactions WHERE Transactions.CustomerID = C.CustomerID ORDER BY TransactionDate DESC) T;  
```

**98. What are partitioned tables in SQL Server, and why use them?**  
- Partitioned tables divide data into partitions for improved query performance and manageability.  
- They are beneficial for large datasets, enabling operations on specific partitions.  
- Example: Partitioned sales data by year for efficient historical queries.  
```sql
CREATE PARTITION FUNCTION pfYear (INT) AS RANGE LEFT FOR VALUES (2019, 2020, 2021);  
CREATE PARTITION SCHEME psYear AS PARTITION pfYear ALL TO ([PRIMARY]);  
CREATE TABLE Sales (SaleID INT, SaleDate DATE, Amount DECIMAL) ON psYear (YEAR(SaleDate));  
```

**99. How do you handle recursive queries in SQL Server?**  
- Use Common Table Expressions (CTEs) with recursion.  
- Useful for traversing hierarchical data like organizational charts.  
- Example: Retrieved all subordinates of a manager in an employee hierarchy.  
```sql
WITH EmployeeHierarchy AS (  
    SELECT EmployeeID, ManagerID FROM Employees WHERE ManagerID IS NULL  
    UNION ALL  
    SELECT E.EmployeeID, E.ManagerID  
    FROM Employees E  
    INNER JOIN EmployeeHierarchy EH ON E.ManagerID = EH.EmployeeID  
)  
SELECT * FROM EmployeeHierarchy;  
```

**100. What is the purpose of the OUTPUT clause in SQL Server?**  
- OUTPUT returns data from modified rows during INSERT, UPDATE, DELETE, or MERGE operations.  
- Helps log changes or retrieve generated values like IDs.  
- Example: Captured deleted records for audit during cleanup.  
```sql
DELETE FROM Orders OUTPUT DELETED.* WHERE OrderDate < '2022-01-01';  
```

**101. What is row-level security in SQL Server?**  
- Row-level security restricts data access at the row level based on user roles or conditions.  
- Implemented using security policies and predicates.  
- Example: Allowed managers to see only their department's records.  
```sql
CREATE SECURITY POLICY SalesPolicy  
ADD FILTER PREDICATE dbo.FilterSales(UserID()) ON Sales;  
```

**102. What is the purpose of the TRY...CATCH block in SQL Server?**  
- TRY...CATCH handles runtime errors in T-SQL scripts or procedures.  
- Ensures graceful error handling and logging.  
- Example: Logged errors during bulk inserts.  
```sql
BEGIN TRY  
    INSERT INTO Sales SELECT * FROM StagingData;  
END TRY  
BEGIN CATCH  
    INSERT INTO ErrorLog (ErrorMessage) VALUES (ERROR_MESSAGE());  
END CATCH;  
```

**103. How do you create a temporary table in SQL Server?**  
- Use `CREATE TABLE` with `#` for local or `##` for global temporary tables.  
- Temporary tables are stored in `tempdb` and automatically dropped.  
- Example: Used a temporary table for intermediate calculations in a complex report.  
```sql
CREATE TABLE #TempSales (ProductID INT, TotalSales DECIMAL);  
INSERT INTO #TempSales SELECT ProductID, SUM(SalesAmount) FROM Sales GROUP BY ProductID;  
```

**104. How do you perform error handling in SQL Server transactions?**  
- Use `TRY...CATCH` with `ROLLBACK` or `COMMIT`.  
- Ensures atomicity by rolling back incomplete transactions.  
- Example: Managed errors during a multi-step order processing transaction.  
```sql
BEGIN TRANSACTION;  
BEGIN TRY  
    INSERT INTO Orders VALUES (1, GETDATE());  
    INSERT INTO OrderDetails VALUES (1, 'ProductA', 2);  
    COMMIT;  
END TRY  
BEGIN CATCH  
    ROLLBACK;  
END CATCH;  
```

**105. What is a surrogate key, and how is it different from a natural key?**  
- A surrogate key is a system-generated unique identifier, often an integer.  
- A natural key is derived from business data and is unique by nature.  
- Example: Used a surrogate key for a Products table instead of product codes.  
```sql
CREATE TABLE Products (ProductID INT IDENTITY(1, 1), ProductCode NVARCHAR(50), Name NVARCHAR(255));  
```

**106. What is the difference between PRIMARY KEY and UNIQUE constraints in SQL?**  
- A PRIMARY KEY uniquely identifies each row and does not allow NULL values.  
- A UNIQUE constraint also ensures uniqueness but allows one NULL value.  
- Example: Used PRIMARY KEY for the `EmployeeID` column and UNIQUE for the `Email` column.  
```sql
CREATE TABLE Employees (  
    EmployeeID INT PRIMARY KEY,  
    Email NVARCHAR(255) UNIQUE  
);  
```

**107. How do you find the second-highest salary in a table?**  
- Use a subquery to exclude the highest salary and retrieve the next highest.  
- Alternative methods include using `OFFSET FETCH` or window functions.  
- Example: Retrieved the second-highest salary using a subquery.  
```sql
SELECT MAX(Salary)  
FROM Employees  
WHERE Salary < (SELECT MAX(Salary) FROM Employees);  
```

**108. What is the purpose of the EXCEPT operator in SQL Server?**  
- The EXCEPT operator returns rows from the first query that are not in the second.  
- It removes duplicates from the result by default.  
- Example: Retrieved customers who have not placed any orders.  
```sql
SELECT CustomerID FROM Customers  
EXCEPT  
SELECT CustomerID FROM Orders;  
```

**109. How do you use PIVOT in SQL Server?**  
- PIVOT rotates table rows into columns for summarization or reporting.  
- Commonly used for creating cross-tabular reports.  
- Example: Summarized sales by year for each region.  
```sql
SELECT Region, [2022] AS Sales2022, [2023] AS Sales2023  
FROM (SELECT Region, Year(SaleDate) AS SaleYear, SalesAmount FROM Sales) AS Source  
PIVOT (SUM(SalesAmount) FOR SaleYear IN ([2022], [2023])) AS PivotTable;  
```

**110. What are SQL Server user-defined types (UDTs)?**  
- UDTs allow you to create reusable data types with specific constraints.  
- Useful for enforcing consistent rules across tables.  
- Example: Created a `PhoneNumber` type for columns that store phone numbers.  
```sql
CREATE TYPE PhoneNumber FROM NVARCHAR(15) NOT NULL;  
CREATE TABLE Customers (CustomerID INT PRIMARY KEY, Contact PhoneNumber);  
```

**111. How do you implement data masking in SQL Server?**  
- Use dynamic data masking to obscure sensitive data for non-privileged users.  
- Masks are applied at the query level, not on stored data.  
- Example: Masked phone numbers for non-admin users.  
```sql
CREATE TABLE Customers (PhoneNumber NVARCHAR(15) MASKED WITH (FUNCTION = 'partial(0,"***-***-",4)'));  
```

**112. What are the different types of backups in SQL Server?**  
- Full: Complete database backup.  
- Differential: Changes since the last full backup.  
- Transaction Log: Logs changes since the last log backup.  
- Example: Automated a full backup nightly and differential backups hourly.  
```sql
BACKUP DATABASE MyDatabase TO DISK = 'C:\Backups\MyDatabase.bak';  
BACKUP LOG MyDatabase TO DISK = 'C:\Backups\MyDatabase_Log.bak';  
```

**113. What are the differences between CHAR and VARCHAR?**  
- CHAR is fixed-length; VARCHAR is variable-length.  
- CHAR is faster for small fixed-size strings, while VARCHAR saves space for varying lengths.  
- Example: Used CHAR for country codes and VARCHAR for descriptions.  
```sql
CREATE TABLE Countries (Code CHAR(3), Name VARCHAR(255));  
```

**114. What is the difference between a heap and a clustered table in SQL Server?**  
- A heap has no clustered index, and rows are stored unordered.  
- A clustered table has a clustered index, and rows are ordered based on the index key.  
- Example: Converted a heap table into a clustered table for faster lookups.  
```sql
CREATE CLUSTERED INDEX IX_Orders_OrderDate ON Orders(OrderDate);  
```

**115. How do you perform string concatenation in SQL Server?**  
- Use the `+` operator or `STRING_AGG` for combining strings.  
- For older versions, use `FOR XML PATH` to concatenate multiple rows.  
- Example: Concatenated employee names from multiple rows.  
```sql
SELECT STRING_AGG(FirstName, ', ') AS Employees  
FROM Employees;  
```

**116. What is the difference between DELETE and TRUNCATE in SQL Server?**  
- DELETE removes rows one by one and can have WHERE conditions; it logs each deletion.  
- TRUNCATE removes all rows quickly without logging individual deletions but cannot have conditions.  
- Example: Used DELETE for specific rows and TRUNCATE for resetting a staging table.  
```sql
DELETE FROM Orders WHERE OrderDate < '2022-01-01';  
TRUNCATE TABLE TempOrders;  
```

**117. How do you create a composite primary key in SQL Server?**  
- Use multiple columns in a PRIMARY KEY constraint.  
- Ensures the combination of columns is unique.  
- Example: Created a composite key for a student-course registration table.  
```sql
CREATE TABLE Registrations (  
    StudentID INT,  
    CourseID INT,  
    PRIMARY KEY (StudentID, CourseID)  
);  
```

**118. What is SQL Server Filestream, and when is it used?**  
- Filestream allows storing and managing unstructured data (like documents and images) in the file system with database integration.  
- Provides transactional consistency for BLOBs stored on the file system.  
- Example: Stored images for product listings using Filestream.  
```sql
CREATE TABLE ProductImages (  
    ProductID INT PRIMARY KEY,  
    Image VARBINARY(MAX) FILESTREAM  
);  
```

**119. How do you use CHECK constraints in SQL Server?**  
- CHECK constraints enforce rules at the column or table level.  
- They ensure data integrity by restricting allowed values.  
- Example: Restricted employee ages to between 18 and 65.  
```sql
CREATE TABLE Employees (  
    EmployeeID INT PRIMARY KEY,  
    Age INT CHECK (Age BETWEEN 18 AND 65)  
);  
```

**120. How do you update multiple tables in SQL Server simultaneously?**  
- Use a transaction to ensure atomic updates.  
- Combine multiple `UPDATE` statements under `BEGIN TRANSACTION`.  
- Example: Updated orders and stock levels atomically.  
```sql
BEGIN TRANSACTION;  
UPDATE Orders SET Status = 'Shipped' WHERE OrderID = 101;  
UPDATE Products SET Stock = Stock - 1 WHERE ProductID = 10;  
COMMIT;  
```  
