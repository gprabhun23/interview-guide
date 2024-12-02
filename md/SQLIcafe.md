### **1. What is a PRIMARY KEY?**  
- Uniquely identifies each record in a table.  
- Ensures that the column(s) contain unique, non-null values.  
- There can only be one primary key per table, which may consist of single or multiple columns.  
- Example: `CREATE TABLE Employee (ID INT PRIMARY KEY, Name NVARCHAR(50));`  

### **2. Define a Temp Table.**  
- A temporary table is a table stored in the `tempdb` database and is available for the current session.  
- It is used to store intermediate results temporarily during query execution.  
- Prefixed with `#` for local temp tables or `##` for global temp tables.  
- Example: `CREATE TABLE #TempTable (ID INT, Name NVARCHAR(50)); INSERT INTO #TempTable VALUES (1, 'John');`  

### **3. What is a VIEW?**  
- A VIEW is a virtual table based on the result of an SQL query.  
- It simplifies complex queries by encapsulating them as reusable objects.  
- Does not store data itself; changes in the base table reflect in the VIEW.  
- Example: `CREATE VIEW EmployeeView AS SELECT ID, Name FROM Employee WHERE Department = 'IT';`  

### **4. What is the DEFAULT constraint?**  
- The DEFAULT constraint sets a default value for a column if no value is provided.  
- It helps maintain consistency in data.  
- Can be applied during table creation or modification.  
- Example: `CREATE TABLE Employee (ID INT, Salary INT DEFAULT 5000);`  

### **5. What is the difference between Data Definition Language (DDL) and Data Manipulation Language (DML)?**  
- DDL deals with schema and structure changes (e.g., `CREATE`, `ALTER`, `DROP`).  
- DML manipulates the data within tables (e.g., `INSERT`, `UPDATE`, `DELETE`).  
- DDL operations are auto-committed, while DML requires explicit commits.  
- Example: DDL: `CREATE TABLE Employee (ID INT);` DML: `INSERT INTO Employee VALUES (1);`  

### **6. What is the difference between TRUNCATE and DELETE?**  
- TRUNCATE removes all rows without logging individual row deletions.  
- DELETE removes rows selectively based on a condition and logs each deletion.  
- TRUNCATE resets identity columns, while DELETE does not.  
- Example: `TRUNCATE TABLE Employee;` vs. `DELETE FROM Employee WHERE ID = 1;`  

### **7. What is a FOREIGN KEY?**  
- A FOREIGN KEY enforces referential integrity between two tables.  
- It establishes a relationship by linking a column to the primary key of another table.  
- Prevents invalid data entry by ensuring related records exist in the referenced table.  
- Example: `CREATE TABLE Orders (OrderID INT, CustomerID INT FOREIGN KEY REFERENCES Customers(CustomerID));`  

### **8. What is Normalization?**  
- Process of organizing database to reduce redundancy and dependency.  
- Divides tables into smaller, logically connected ones.  
- Ensures data integrity and efficient updates.  
- Example: In my project, I normalized customer data into separate tables for Customers and Orders.  

### **9. What is Denormalization?**  
- Process of combining normalized tables to optimize read performance.  
- Introduces redundancy to reduce the complexity of joins.  
- Used in OLAP systems for faster query execution.  
- Example: Denormalized Customer and Order tables into one for reporting performance.  

### **10. What is the difference between the WHERE clause and the HAVING clause?**  
- WHERE filters rows before grouping, HAVING filters after grouping.  
- WHERE cannot work with aggregate functions; HAVING can.  
- Both can be used together in the same query.  
- Example: `SELECT Department, AVG(Salary) FROM Employee GROUP BY Department HAVING AVG(Salary) > 5000;`  

### **11. What is the difference between JOIN and UNION?**  
- JOIN combines columns from related tables, UNION combines rows from queries.  
- JOIN needs a relationship between tables, UNION works on independent results.  
- UNION removes duplicates by default; UNION ALL retains all rows.  
- Example: `SELECT Name FROM Employee UNION SELECT Name FROM Manager;`  

### **12. What are the differences between Clustered and Non-clustered indexes?**  
- Clustered index sorts and stores data rows; non-clustered does not.  
- A table can have only one clustered index but multiple non-clustered indexes.  
- Clustered index is faster for range queries; non-clustered for exact lookups.  
- Example: `CREATE CLUSTERED INDEX IX_Employee ON Employee(ID);`  

### **13. How does a Hash index work?**  
- Uses a hash function to map keys to a location in the index.  
- Efficient for equality searches but not suitable for range queries.  
- Requires space for hash tables in memory or disk.  
- Example: Used hash indexing for quick lookup in a large user authentication table.  

### **14. What is the difference between INNER JOIN and OUTER JOIN?**  
- INNER JOIN returns matching rows from both tables.  
- OUTER JOIN includes unmatched rows from one or both tables, depending on type.  
- Types: LEFT OUTER, RIGHT OUTER, FULL OUTER JOIN.  
- Example: `SELECT e.Name, d.Name FROM Employee e LEFT JOIN Department d ON e.DeptID = d.ID;`  

### **15. What is Collation in SQL?**  
- Collation defines rules for text sorting and comparison.  
- Includes sensitivity to case, accents, and locale-specific rules.  
- Important for multilingual databases.  
- Example: `SELECT * FROM Employee WHERE Name COLLATE Latin1_General_BIN = 'john';`  

### **16. What's the difference between a Primary Key and a Unique Key?**  
- Primary Key enforces uniqueness and non-null constraints; Unique Key allows one NULL value.  
- A table can have only one Primary Key but multiple Unique Keys.  
- Primary Key creates a clustered index by default; Unique Key creates a non-clustered index.  
- Example: `CREATE TABLE Employee (ID INT PRIMARY KEY, Email NVARCHAR(50) UNIQUE);`  

### **17. How can a VIEW be used to provide a security layer for your app?**  
- Restricts access by exposing only necessary columns or rows.  
- Encapsulates complex logic, hiding table structure from users.  
- Prevents direct access to base tables and sensitive data.  
- Example: `CREATE VIEW PublicEmployeeData AS SELECT Name, Department FROM Employee;`  

### **18. What’s the difference between Azure SQL Database and Azure SQL Managed Instance?**  
- Azure SQL Database is a PaaS offering for single databases; Managed Instance is for near full SQL Server compatibility.  
- Managed Instance supports features like cross-database queries and SQL Agent.  
- SQL Database is more cost-effective for isolated workloads; Managed Instance suits enterprise applications.  
- Example: I used Azure SQL Database for an e-commerce app with independent databases.  

### **19. How can a database index help performance?**  
- Speeds up data retrieval by reducing the number of rows scanned.  
- Organizes data for efficient search and filtering operations.  
- Impacts write operations slightly due to index maintenance.  
- Example: Added indexes to optimize search queries for product inventory in a retail app.  

### **20. Discuss INNER JOIN vs WHERE clause (with multiple FROM tables).**  
- INNER JOIN explicitly defines relationships; WHERE filters results.  
- INNER JOIN is more readable and declarative.  
- For multiple FROM tables, INNER JOIN avoids Cartesian products.  
- Example: `SELECT e.Name, d.Name FROM Employee e INNER JOIN Department d ON e.DeptID = d.ID;`  

### **21. Define ACID Properties.**  
- Atomicity ensures transactions are all-or-nothing.  
- Consistency maintains database integrity.  
- Isolation ensures concurrent transactions don’t interfere.  
- Durability guarantees persistence of committed data.  
- Example: Used ACID-compliant databases to handle financial transactions securely.  

### **22. Describe the difference between TRUNCATE and DELETE.**  
- TRUNCATE removes all rows without logging row deletions.  
- DELETE selectively removes rows and logs each action.  
- TRUNCATE resets identity columns, DELETE does not.  
- Example: Used DELETE to remove expired coupons while retaining history logs.  

### **23. What is the difference between UNION and UNION ALL?**  
- UNION removes duplicate rows; UNION ALL retains all rows.  
- UNION requires additional processing for duplicate elimination.  
- UNION ALL is faster due to no deduplication.  
- Example: `SELECT Name FROM Employee UNION ALL SELECT Name FROM Contractor;`  

### **24. What is the difference between INNER JOIN, OUTER JOIN, and FULL OUTER JOIN?**  
- INNER JOIN retrieves matching rows from both tables.  
- OUTER JOIN includes unmatched rows from one table (LEFT or RIGHT).  
- FULL OUTER JOIN includes unmatched rows from both tables.  
- Example: `SELECT e.Name, d.Name FROM Employee e FULL OUTER JOIN Department d ON e.DeptID = d.ID;`  

### **25. What is the cost of having a database index?**  
- Additional storage for index structure.  
- Increased write operation time due to index maintenance.  
- Potential performance degradation if over-indexed.  
- Example: Balanced indexes to improve search times without hindering batch inserts in an analytics database.  

### **26. What is faster, one big query or many small queries?**  
- One big query minimizes network overhead but can be harder to debug.  
- Small queries are modular but increase network and processing overhead.  
- Depends on the use case and database engine optimization.  
- Example: Used one big query with CTEs for generating monthly sales reports efficiently.  

### **27. Explain the difference between Exclusive Lock and Update Lock.**  
- Exclusive Lock prevents other operations from accessing the resource.  
- Update Lock allows reads but prevents multiple updates.  
- Update Lock reduces deadlocks compared to Exclusive Lock.  
- Example: Used Update Locks to handle inventory updates without impacting read operations.  

### **28. How does a B-trees Index work?**  
- B-trees organize data hierarchically for efficient retrieval.  
- Balanced structure ensures uniform search time across nodes.  
- Supports range queries and ordered retrieval.  
- Example: Leveraged B-tree indexing to speed up searches on large customer datasets.  

### **29. What is the difference among UNION, MINUS, and INTERSECT?**  
- UNION combines distinct rows from two queries.  
- MINUS retrieves rows in the first query not in the second.  
- INTERSECT retrieves rows common to both queries.  
- Example: `SELECT Name FROM Employee MINUS SELECT Name FROM RetiredEmployees;`  

### **30. What are some other types of Indexes (vs B-Trees)?**  
- Hash Index: Efficient for equality searches.  
- Bitmap Index: Optimized for low-cardinality columns.  
- Full-text Index: Specialized for textual data and keyword searches.  
- Example: Used a Full-text Index for implementing search functionality in a document management system.  

### **31. How does database indexing work?**  
- Indexing creates a data structure to speed up query retrieval by avoiding full table scans.  
- It uses B-trees, hash tables, or other structures to map values to storage locations.  
- Indexes improve read performance but can slow down write operations due to maintenance.  
- Example: Added an index on the `Email` column to optimize user login queries.  

### **32. What is the difference between Optimistic Locking and Pessimistic Locking?**  
- Optimistic Locking assumes minimal conflicts and validates data during updates.  
- Pessimistic Locking prevents conflicts by locking data until the transaction completes.  
- Optimistic Locking is suitable for high-concurrency systems; Pessimistic for critical updates.  
- Example: Used Optimistic Locking for resolving simultaneous edits in a collaborative app.  

### **33. Name some disadvantages of a Hash index.**  
- Not suitable for range queries.  
- Requires extra memory for hash tables.  
- Poor performance for highly skewed data distributions.  
- Example: Encountered inefficiencies using hash indexing for customer age range searches.  

### **34. What is the difference between B-Tree, R-Tree, and Hash indexing?**  
- B-Tree supports range queries and ordered data.  
- R-Tree is optimized for multi-dimensional data like GIS applications.  
- Hash indexing excels in exact match lookups but not ordered retrievals.  
- Example: Used B-Tree for product searches and R-Tree for geolocation queries in my app.  

### **35. What is Index Cardinality, and why does it matter?**  
- Index cardinality refers to the uniqueness of values in a column.  
- High cardinality improves index efficiency for searches and lookups.  
- Low cardinality may lead to performance issues due to redundancy.  
- Example: Indexed high-cardinality columns like `CustomerID` to speed up retrievals.  

### **36. How to select the first 5 records from a table?**  
- Use the `TOP` keyword in SQL Server or `LIMIT` in MySQL.  
- Orders results to ensure consistent output.  
- May use `FETCH` and `OFFSET` for pagination.  
- Example: `SELECT TOP 5 * FROM Employee ORDER BY Salary DESC;`  

### **37. Find duplicate values in a SQL table.**  
- Use `GROUP BY` and `HAVING` to identify duplicates.  
- Aggregate the data to find repeated values.  
- Use `COUNT` to highlight rows with duplicates.  
- Example: `SELECT Name, COUNT(*) FROM Employee GROUP BY Name HAVING COUNT(*) > 1;`  

### **38. How can we transpose a table using SQL (changing rows to columns or vice-versa)?**  
- Use `PIVOT` to convert rows to columns.  
- Use `UNPIVOT` to convert columns to rows.  
- Requires aggregating data for transformation.  
- Example: `SELECT * FROM (SELECT Department, Salary FROM Employee) AS SourceTable PIVOT (SUM(Salary) FOR Department IN ([IT], [HR], [Sales])) AS PivotTable;`  

### **39. How to generate a row number in SQL without using ROWNUM?**  
- Use the `ROW_NUMBER()` function in SQL Server.  
- It assigns unique sequential numbers to each row based on a specified order.  
- Supports ordering and partitioning.  
- Example: `SELECT ROW_NUMBER() OVER (ORDER BY Salary DESC) AS RowNum, Name FROM Employee;`  

### **40. What would happen without an Index?**  
- Full table scans would be required for every query.  
- Query performance would degrade with larger datasets.  
- Increased CPU and IO utilization for retrievals.  
- Example: Optimized a reporting query by adding indexes, reducing runtime from minutes to seconds.  

### **41. Delete duplicate values in a SQL table.**  
- Use `CTE` or subqueries to identify duplicates.  
- Delete duplicates while retaining the desired rows.  
- Use `ROW_NUMBER()` to flag duplicates.  
- Example:  
```sql  
WITH CTE AS (  
  SELECT Name, ROW_NUMBER() OVER (PARTITION BY Name ORDER BY ID) AS RowNum  
  FROM Employee  
)  
DELETE FROM CTE WHERE RowNum > 1;  
```  

### **42. How do TRUNCATE and DELETE operations affect Identity columns?**  
- TRUNCATE resets the identity seed to the default value.  
- DELETE does not affect the identity seed.  
- Use `DBCC CHECKIDENT` to reset identity manually.  
- Example: Used `TRUNCATE` on a test table to reset identity during data preparation.  

### **43. How can I do an UPDATE statement with a JOIN in SQL?**  
- Use `JOIN` in the `UPDATE` statement to modify data based on related tables.  
- Specify the target table and the join condition.  
- Include a `SET` clause to define updates.  
- Example:  
```sql  
UPDATE e  
SET e.Salary = e.Salary * 1.1  
FROM Employee e  
INNER JOIN Department d ON e.DeptID = d.ID  
WHERE d.Name = 'IT';  
```  

### **44. Select the first row in each GROUP BY group (greatest-n-per-group problem).**  
- Use `ROW_NUMBER()` or `RANK()` to rank rows within groups.  
- Filter rows where the rank equals 1.  
- Useful for deduplication or summary queries.  
- Example:  
```sql  
WITH CTE AS (  
  SELECT Name, Department, ROW_NUMBER() OVER (PARTITION BY Department ORDER BY Salary DESC) AS RowNum  
  FROM Employee  
)  
SELECT * FROM CTE WHERE RowNum = 1;  
```  

### **45. How can we efficiently manage indexing in a database?**  
- Regularly monitor index usage with DMVs or tools.  
- Remove unused or redundant indexes.  
- Rebuild or reorganize fragmented indexes.  
- Example: Scheduled monthly index maintenance to ensure optimal query performance.  