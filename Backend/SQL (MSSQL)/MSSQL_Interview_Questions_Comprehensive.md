# 🎯 MSSQL Interview Questions - Comprehensive Guide

## 📋 Table of Contents
1. [Basics & Fundamentals](#basics)
2. [Data Types & Storage](#datatypes)
3. [DDL (Data Definition Language)](#ddl)
4. [DML (Data Manipulation Language)](#dml)
5. [Queries & JOINs](#queries)
6. [Indexes & Performance](#indexes)
7. [Views, Stored Procedures & Functions](#advanced)
8. [Transactions & Locks](#transactions)
9. [Backup & Recovery](#backup)
10. [Real-World Scenarios](#scenarios)

---

## <a id="basics"></a>## 1️⃣ BASICS & FUNDAMENTALS

### Q1: What is SQL Server and its key features?
**Answer:**
SQL Server is a relational database management system (RDBMS) developed by Microsoft.

**Key Features:**
- ✅ Relational database with ACID compliance
- ✅ High availability and disaster recovery
- ✅ Strong security features
- ✅ Scalability and performance
- ✅ Integration with .NET ecosystem
- ✅ Advanced analytics and reporting
- ✅ Cloud-ready (Azure SQL)

```sql
-- Check SQL Server version
SELECT @@VERSION;
```

---

### Q2: What are the differences between SQL Server, MySQL, and PostgreSQL?

| Feature | SQL Server | MySQL | PostgreSQL |
|---------|-----------|-------|-----------|
| **Owner** | Microsoft | Oracle | Open Source |
| **License** | Proprietary/Free Express | Open Source | Open Source |
| **ACID Compliance** | ✅ Full | ✅ Full (InnoDB) | ✅ Full |
| **Scalability** | Enterprise | Good | Excellent |
| **Windows Support** | Native | Good | Good |
| **Cost** | High (Standard/Enterprise) | Free | Free |
| **Performance** | Excellent | Good | Excellent |

---

### Q3: What is a database and what are its main components?
**Answer:**

A database is an organized collection of structured data stored and retrieved electronically.

**Main Components:**
1. **Tables** - Store data in rows and columns
2. **Indexes** - Speed up data retrieval
3. **Views** - Virtual tables for simplified queries
4. **Stored Procedures** - Reusable SQL code
5. **Triggers** - Automatic actions on table events
6. **Keys** - Primary, Foreign, Unique constraints
7. **Schemas** - Logical organization of objects

---

### Q4: What is the difference between a Database and a Schema?

| Database | Schema |
|----------|--------|
| Collection of related data | Logical container within a database |
| Physical storage unit | Organizes tables, views, procedures |
| Can contain multiple schemas | Belongs to one database |
| Server-level object | Database-level object |

```sql
-- Create a schema
CREATE SCHEMA HR;

-- Create table in schema
CREATE TABLE HR.Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100)
);

-- Query from schema
SELECT * FROM HR.Employees;
```

---

### Q5: What are the ACID properties in databases?

**ACID = Atomicity, Consistency, Isolation, Durability**

| Property | Meaning | Example |
|----------|---------|---------|
| **Atomicity** | Transaction is "all or nothing" | Transfer money: debit & credit both succeed or both fail |
| **Consistency** | Data moves from valid to valid state | Account balance never goes negative |
| **Isolation** | Transactions don't interfere | User A's changes don't affect User B's query |
| **Durability** | Committed data survives failures | After COMMIT, data persists even after crash |

```sql
BEGIN TRANSACTION;
  UPDATE Accounts SET Balance = Balance - 100 WHERE AccountID = 1;
  UPDATE Accounts SET Balance = Balance + 100 WHERE AccountID = 2;
COMMIT;
```

---

## <a id="datatypes"></a>## 2️⃣ DATA TYPES & STORAGE

### Q6: What are the main data types in SQL Server?

**Numeric Data Types:**
```sql
INT              -- Integer (-2^31 to 2^31-1)
BIGINT           -- Large integer
FLOAT            -- Floating point
DECIMAL(p,s)     -- Fixed precision (price: DECIMAL(10,2))
MONEY            -- Currency
TINYINT          -- 0-255
SMALLINT         -- Small integer
```

**String Data Types:**
```sql
CHAR(n)          -- Fixed length string
VARCHAR(n)       -- Variable length string (up to n)
NCHAR(n)         -- Unicode fixed length
NVARCHAR(n)      -- Unicode variable length
TEXT             -- Large text (deprecated, use VARCHAR(MAX))
```

**Date/Time Data Types:**
```sql
DATE             -- Only date (2025-05-27)
TIME             -- Only time (14:30:45)
DATETIME         -- Date and time
DATETIME2        -- More precise datetime
SMALLDATETIME    -- Less precise
DATEFROMPARTS()  -- Create date
GETDATE()        -- Current date/time
```

**Other Data Types:**
```sql
BIT              -- Boolean (0 or 1)
BINARY(n)        -- Fixed binary
IMAGE            -- Large binary (deprecated)
XML              -- XML data
JSON             -- JSON format (SQL Server 2016+)
```

---

### Q7: What's the difference between CHAR, VARCHAR, and NVARCHAR?

```sql
-- CHAR: Fixed length, space-padded
CHAR(10) 'Hello'     -- Stored as 'Hello     ' (5 chars + 5 spaces)

-- VARCHAR: Variable length, no padding
VARCHAR(10) 'Hello'  -- Stored as 'Hello' (5 chars only)

-- NVARCHAR: Unicode variable length (supports all languages)
NVARCHAR(10) 'Hello' -- Supports Chinese, Arabic, etc.
```

**When to use:**
- **CHAR**: Fixed-size data (Country codes: 'US', 'IN')
- **VARCHAR**: Variable-size data (Names, Addresses)
- **NVARCHAR**: International characters needed

---

### Q8: What is NULL in SQL Server and how is it different from empty string?

```sql
-- NULL = No value, unknown
SELECT NULL;         -- NULL (missing data)

-- Empty string = Zero-length string
SELECT '';           -- Empty string ''

-- Difference
SELECT NULL = '';    -- NULL (comparison with NULL is always NULL)
SELECT NULL IS NULL; -- TRUE

-- Checking for NULL
SELECT * FROM Users WHERE MiddleName IS NULL;
SELECT * FROM Users WHERE MiddleName IS NOT NULL;

-- ISNULL function
SELECT ISNULL(MiddleName, 'N/A') FROM Users;
```

---

## <a id="ddl"></a>## 3️⃣ DDL (DATA DEFINITION LANGUAGE)

### Q9: What are DDL commands? Give examples.

**DDL = CREATE, ALTER, DROP, TRUNCATE**

```sql
-- CREATE: Create new table
CREATE TABLE Products (
    ProductID INT PRIMARY KEY IDENTITY(1,1),
    ProductName VARCHAR(100) NOT NULL,
    Price DECIMAL(10,2) CHECK (Price > 0),
    CreatedDate DATETIME DEFAULT GETDATE()
);

-- ALTER: Modify table structure
ALTER TABLE Products ADD Category VARCHAR(50);
ALTER TABLE Products DROP COLUMN Category;
ALTER TABLE Products ALTER COLUMN ProductName VARCHAR(200);

-- DROP: Delete table and structure
DROP TABLE Products;

-- TRUNCATE: Delete all rows (faster than DELETE)
TRUNCATE TABLE Products;  -- Resets IDENTITY
```

**Difference: DROP vs DELETE vs TRUNCATE**

| Command | Removes | Space | IDENTITY | Speed | Rollback |
|---------|---------|-------|----------|-------|----------|
| **DROP** | Table + Data | Yes | Reset | Fast | ✅ (Uncommitted) |
| **DELETE** | Rows only | No | No | Slow | ✅ (In transaction) |
| **TRUNCATE** | Rows only | Yes | Reset | Fast | ✅ (Uncommitted) |

---

### Q10: What are constraints and how many types are there?

**Constraints = Rules enforced on columns/tables**

```sql
CREATE TABLE Employees (
    -- PRIMARY KEY: Unique + Not Null
    EmployeeID INT PRIMARY KEY,
    
    -- UNIQUE: No duplicate values
    Email VARCHAR(100) UNIQUE,
    
    -- NOT NULL: Cannot be empty
    EmployeeName VARCHAR(100) NOT NULL,
    
    -- DEFAULT: Default value if not provided
    JoinDate DATETIME DEFAULT GETDATE(),
    
    -- CHECK: Validate data
    Salary DECIMAL(10,2) CHECK (Salary > 0),
    
    -- FOREIGN KEY: Reference another table
    DepartmentID INT FOREIGN KEY REFERENCES Departments(DepartmentID),
    
    -- Multiple columns as PRIMARY KEY
    CONSTRAINT PK_Employee PRIMARY KEY (EmployeeID, Email)
);
```

---

### Q11: What is the difference between PRIMARY KEY and UNIQUE constraint?

| Feature | PRIMARY KEY | UNIQUE |
|---------|-------------|--------|
| **NULL values** | Not allowed | Allowed (multiple NULLs) |
| **Count per table** | Only 1 | Multiple allowed |
| **Purpose** | Identify rows uniquely | Prevent duplicates |
| **Index** | Creates clustered index | Creates non-clustered index |
| **Foreign Key** | Can reference | Cannot reference |

```sql
CREATE TABLE Users (
    UserID INT PRIMARY KEY,      -- Unique identifier
    Email VARCHAR(100) UNIQUE,   -- No duplicate emails
    Phone VARCHAR(15) UNIQUE     -- No duplicate phones
);
```

---

### Q12: What is IDENTITY and how does it work?

```sql
CREATE TABLE Products (
    ProductID INT PRIMARY KEY IDENTITY(1, 1),  -- Start at 1, increment by 1
    ProductName VARCHAR(100)
);

-- Insert without specifying ProductID
INSERT INTO Products (ProductName) VALUES ('Laptop');  -- ProductID = 1
INSERT INTO Products (ProductName) VALUES ('Mouse');   -- ProductID = 2

-- View last inserted ID
SELECT @@IDENTITY;
SELECT SCOPE_IDENTITY();
SELECT IDENT_CURRENT('Products');

-- Reset IDENTITY
DBCC CHECKIDENT (Products, RESEED, 0);

-- Insert with specific ID
SET IDENTITY_INSERT Products ON;
INSERT INTO Products (ProductID, ProductName) VALUES (100, 'Keyboard');
SET IDENTITY_INSERT Products OFF;
```

---

## <a id="dml"></a>## 4️⃣ DML (DATA MANIPULATION LANGUAGE)

### Q13: What are DML commands?

**DML = INSERT, UPDATE, DELETE, SELECT**

```sql
-- INSERT: Add new data
INSERT INTO Products (ProductName, Price) 
VALUES ('Laptop', 50000);

INSERT INTO Products (ProductName, Price) 
VALUES 
    ('Mouse', 500),
    ('Keyboard', 2000),
    ('Monitor', 15000);

-- INSERT from SELECT
INSERT INTO Products_Backup
SELECT * FROM Products WHERE Price > 10000;

-- UPDATE: Modify existing data
UPDATE Products 
SET Price = 55000 
WHERE ProductName = 'Laptop';

UPDATE Products
SET Price = Price * 1.1;  -- Increase all prices by 10%

-- DELETE: Remove data
DELETE FROM Products 
WHERE ProductID = 1;

DELETE FROM Products;  -- Delete all rows (slow, logs each deletion)

-- SELECT: Retrieve data
SELECT * FROM Products;
SELECT ProductName, Price FROM Products WHERE Price > 1000;
```

---

### Q14: What's the difference between INSERT and SELECT...INSERT?

```sql
-- INSERT: Add specific values
INSERT INTO Products (ProductName, Price) 
VALUES ('Laptop', 50000);

-- SELECT...INSERT: Copy data from another table
INSERT INTO Products_Archive 
SELECT * FROM Products 
WHERE Price > 50000;  -- Only expensive products

-- Useful for backup, migration, or data transformation
INSERT INTO Audit_Log (Action, DateTime)
SELECT 'Product Added', GETDATE()
FROM Products WHERE ProductID = SCOPE_IDENTITY();
```

---

### Q15: What is the UPDATE statement with JOINs?

```sql
-- Update based on joined table
UPDATE p
SET p.Category = c.CategoryName
FROM Products p
INNER JOIN Categories c ON p.CategoryID = c.CategoryID
WHERE c.CategoryName = 'Electronics';

-- Update multiple columns
UPDATE Employees
SET 
    Salary = Salary * 1.1,
    UpdatedDate = GETDATE()
WHERE DepartmentID = 1;

-- Update with CTE
WITH HighPriceProducts AS (
    SELECT ProductID FROM Products WHERE Price > 50000
)
UPDATE Products
SET Discount = 10
FROM HighPriceProducts h
WHERE h.ProductID = Products.ProductID;
```

---

### Q16: What is a transaction? How do you use COMMIT and ROLLBACK?

```sql
-- Begin transaction
BEGIN TRANSACTION;

    INSERT INTO Accounts VALUES (1, 'John', 1000);
    INSERT INTO Accounts VALUES (2, 'Jane', 2000);
    
    -- If everything is OK
    COMMIT;  -- Save all changes
    
    -- If something goes wrong
    ROLLBACK;  -- Undo all changes

-- Example with error handling
BEGIN TRANSACTION;
BEGIN TRY
    UPDATE Accounts SET Balance = Balance - 100 WHERE AccountID = 1;
    UPDATE Accounts SET Balance = Balance + 100 WHERE AccountID = 2;
    COMMIT;
    PRINT 'Transaction successful';
END TRY
BEGIN CATCH
    ROLLBACK;
    PRINT 'Transaction failed: ' + ERROR_MESSAGE();
END CATCH;

-- Savepoint (partial rollback)
BEGIN TRANSACTION;
    INSERT INTO Table1 VALUES (1);
    SAVE TRANSACTION SP1;
    
    INSERT INTO Table2 VALUES (1);  -- If this fails
    ROLLBACK TRANSACTION SP1;  -- Only rollback to SP1
    
COMMIT;
```

---

## <a id="queries"></a>## 5️⃣ QUERIES & JOINs

### Q17: What are the different types of JOINs?

```sql
-- INNER JOIN: Only matching rows from both tables
SELECT 
    e.EmployeeName,
    d.DepartmentName
FROM Employees e
INNER JOIN Departments d ON e.DepartmentID = d.DepartmentID;

-- LEFT JOIN: All rows from left table + matching from right
SELECT 
    e.EmployeeName,
    d.DepartmentName
FROM Employees e
LEFT JOIN Departments d ON e.DepartmentID = d.DepartmentID;
-- Returns employees even if they have no department

-- RIGHT JOIN: All rows from right table + matching from left
SELECT 
    e.EmployeeName,
    d.DepartmentName
FROM Employees e
RIGHT JOIN Departments d ON e.DepartmentID = d.DepartmentID;

-- FULL OUTER JOIN: All rows from both tables
SELECT 
    e.EmployeeName,
    d.DepartmentName
FROM Employees e
FULL OUTER JOIN Departments d ON e.DepartmentID = d.DepartmentID;

-- CROSS JOIN: Cartesian product (all combinations)
SELECT 
    e.EmployeeName,
    p.ProductName
FROM Employees e
CROSS JOIN Products p;
-- If 10 employees and 5 products = 50 rows

-- SELF JOIN: Join table to itself
SELECT 
    e1.EmployeeName AS Employee,
    e2.EmployeeName AS Manager
FROM Employees e1
LEFT JOIN Employees e2 ON e1.ManagerID = e2.EmployeeID;
```

---

### Q18: What are aggregate functions and how are they used?

```sql
-- COUNT: Number of rows
SELECT COUNT(*) AS TotalEmployees FROM Employees;
SELECT COUNT(ManagerID) AS EmployeesWithManager FROM Employees;

-- SUM: Total of numeric column
SELECT SUM(Salary) AS TotalSalaryExpense FROM Employees;

-- AVG: Average value
SELECT AVG(Salary) AS AverageSalary FROM Employees;

-- MIN/MAX: Minimum and maximum
SELECT 
    MIN(Salary) AS LowestSalary,
    MAX(Salary) AS HighestSalary
FROM Employees;

-- GROUP BY: Aggregate by groups
SELECT 
    DepartmentID,
    COUNT(*) AS EmployeeCount,
    AVG(Salary) AS AvgSalary
FROM Employees
GROUP BY DepartmentID;

-- HAVING: Filter groups (WHERE filters rows, HAVING filters groups)
SELECT 
    DepartmentID,
    COUNT(*) AS EmployeeCount
FROM Employees
GROUP BY DepartmentID
HAVING COUNT(*) > 5;  -- Only departments with more than 5 employees

-- Multiple aggregate functions
SELECT 
    DepartmentID,
    COUNT(*) AS EmployeeCount,
    SUM(Salary) AS TotalSalary,
    AVG(Salary) AS AvgSalary,
    MIN(Salary) AS MinSalary,
    MAX(Salary) AS MaxSalary
FROM Employees
GROUP BY DepartmentID;
```

---

### Q19: What is GROUP BY and HAVING? What's the difference?

```sql
-- GROUP BY: Organizes rows into groups
-- HAVING: Filters groups (applied after GROUP BY)

SELECT 
    DepartmentID,
    COUNT(*) AS EmployeeCount,
    AVG(Salary) AS AvgSalary
FROM Employees
WHERE Salary > 30000       -- WHERE filters rows BEFORE grouping
GROUP BY DepartmentID
HAVING COUNT(*) > 3        -- HAVING filters groups AFTER grouping
ORDER BY AvgSalary DESC;

-- Without GROUP BY (entire table is one group)
SELECT 
    COUNT(*) AS TotalEmployees,
    AVG(Salary) AS AvgSalary
FROM Employees;

-- Common mistake: Selecting column not in GROUP BY
-- This will error if column is not aggregated:
-- SELECT DepartmentID, EmployeeName, COUNT(*)  -- ERROR!
-- SELECT DepartmentID, COUNT(*) -- OK
```

---

### Q20: What is the difference between WHERE and HAVING?

| WHERE | HAVING |
|-------|--------|
| Filters rows BEFORE grouping | Filters groups AFTER grouping |
| Used with SELECT, UPDATE, DELETE | Used only with GROUP BY |
| Operates on columns | Operates on aggregate functions |
| Can reference any column | Can reference only grouped/aggregated columns |
| More efficient (filters early) | Less efficient (filters late) |

```sql
-- Incorrect: Can't use HAVING without GROUP BY
SELECT * FROM Employees HAVING Salary > 50000;  -- ERROR

-- WHERE filters individual rows
SELECT * FROM Employees WHERE Salary > 50000;   -- OK

-- GROUP BY + HAVING
SELECT DepartmentID, COUNT(*) 
FROM Employees
GROUP BY DepartmentID
HAVING COUNT(*) > 5;
```

---

### Q21: What are window functions? Give examples.

```sql
-- ROW_NUMBER: Unique number for each row
SELECT 
    EmployeeName,
    Salary,
    ROW_NUMBER() OVER (ORDER BY Salary DESC) AS SalaryRank
FROM Employees;

-- RANK: Rank with gaps if ties exist
SELECT 
    EmployeeName,
    Salary,
    RANK() OVER (ORDER BY Salary DESC) AS SalaryRank
FROM Employees;

-- DENSE_RANK: Rank without gaps
SELECT 
    EmployeeName,
    Salary,
    DENSE_RANK() OVER (ORDER BY Salary DESC) AS SalaryRank
FROM Employees;

-- PARTITION BY: Window functions per group
SELECT 
    EmployeeName,
    DepartmentID,
    Salary,
    RANK() OVER (PARTITION BY DepartmentID ORDER BY Salary DESC) AS DeptSalaryRank
FROM Employees;

-- LAG/LEAD: Previous/Next row value
SELECT 
    EmployeeName,
    Salary,
    LAG(Salary) OVER (ORDER BY Salary) AS PreviousSalary,
    LEAD(Salary) OVER (ORDER BY Salary) AS NextSalary
FROM Employees;

-- Running sum
SELECT 
    EmployeeName,
    Salary,
    SUM(Salary) OVER (ORDER BY EmployeeID 
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS RunningTotal
FROM Employees;
```

---

### Q22: What is DISTINCT and how does it work?

```sql
-- DISTINCT: Remove duplicate rows
SELECT DISTINCT City FROM Employees;
-- Returns unique cities only

-- With multiple columns
SELECT DISTINCT DepartmentID, City FROM Employees;
-- Returns unique combinations

-- With aggregate
SELECT COUNT(DISTINCT City) AS UniqueCities FROM Employees;

-- DISTINCT in ORDER BY
SELECT DISTINCT 
    City,
    DepartmentID
FROM Employees
ORDER BY City;

-- Difference
SELECT City FROM Employees;           -- All cities (duplicates)
SELECT DISTINCT City FROM Employees;  -- Unique cities only
```

---

### Q23: What is UNION, UNION ALL, INTERSECT, and EXCEPT?

```sql
-- UNION: Combine results, remove duplicates
SELECT City FROM Employees
UNION
SELECT City FROM Customers;
-- Returns unique cities from both tables

-- UNION ALL: Combine results, keep duplicates (faster)
SELECT City FROM Employees
UNION ALL
SELECT City FROM Customers;

-- INTERSECT: Common rows in both result sets
SELECT City FROM Employees
INTERSECT
SELECT City FROM Customers;
-- Returns cities that exist in both tables

-- EXCEPT: Rows in first but not in second
SELECT City FROM Employees
EXCEPT
SELECT City FROM Customers;
-- Returns cities in Employees but not in Customers

-- All three must have same number of columns with compatible types
SELECT EmployeeID, EmployeeName FROM Employees
UNION
SELECT CustomerID, CustomerName FROM Customers;
-- Column names from first query are used
```

---

### Q24: What is a subquery (nested query)?

```sql
-- Subquery in WHERE clause
SELECT * FROM Employees
WHERE Salary > (SELECT AVG(Salary) FROM Employees);
-- Employees earning more than average

-- Subquery in FROM clause (derived table)
SELECT * FROM (
    SELECT DepartmentID, COUNT(*) AS EmployeeCount
    FROM Employees
    GROUP BY DepartmentID
) AS DeptCount
WHERE EmployeeCount > 5;

-- Subquery with IN
SELECT * FROM Employees
WHERE DepartmentID IN (
    SELECT DepartmentID FROM Departments 
    WHERE DepartmentName LIKE '%IT%'
);

-- Correlated subquery (references outer query)
SELECT 
    e1.EmployeeName,
    e1.Salary,
    (SELECT COUNT(*) FROM Employees e2 
     WHERE e2.DepartmentID = e1.DepartmentID) AS DeptHeadcount
FROM Employees e1;

-- EXISTS: Check if subquery returns any rows
SELECT * FROM Employees e
WHERE EXISTS (
    SELECT 1 FROM Orders o 
    WHERE o.CustomerID = e.EmployeeID
);
```

---

### Q25: What is a CTE (Common Table Expression)?

```sql
-- Simple CTE
WITH EmployeeAverage AS (
    SELECT AVG(Salary) AS AvgSalary FROM Employees
)
SELECT 
    EmployeeName,
    Salary,
    (SELECT AvgSalary FROM EmployeeAverage) AS CompanyAverage
FROM Employees;

-- Multiple CTEs
WITH DeptStats AS (
    SELECT DepartmentID, COUNT(*) AS EmpCount, AVG(Salary) AS AvgSal
    FROM Employees
    GROUP BY DepartmentID
),
HighEarners AS (
    SELECT EmployeeID, EmployeeName, Salary
    FROM Employees
    WHERE Salary > 100000
)
SELECT 
    e.EmployeeName,
    e.Salary,
    d.AvgSal
FROM HighEarners e
JOIN DeptStats d ON e.EmployeeID = d.DepartmentID;

-- Recursive CTE (hierarchy)
WITH EmployeeHierarchy AS (
    -- Base case: CEO (no manager)
    SELECT EmployeeID, EmployeeName, ManagerID, 0 AS Level
    FROM Employees
    WHERE ManagerID IS NULL
    
    UNION ALL
    
    -- Recursive case: Direct reports
    SELECT e.EmployeeID, e.EmployeeName, e.ManagerID, Level + 1
    FROM Employees e
    INNER JOIN EmployeeHierarchy eh ON e.ManagerID = eh.EmployeeID
)
SELECT * FROM EmployeeHierarchy;
```

---

## <a id="indexes"></a>## 6️⃣ INDEXES & PERFORMANCE

### Q26: What are indexes and their types?

```sql
-- Clustered Index: Physical order of data (only 1 per table)
CREATE CLUSTERED INDEX IX_Employee_ID 
ON Employees(EmployeeID);

-- Non-Clustered Index: Separate structure (up to 999 per table)
CREATE NONCLUSTERED INDEX IX_Employee_Name
ON Employees(EmployeeName);

-- Unique Index: Ensures uniqueness
CREATE UNIQUE NONCLUSTERED INDEX IX_Employee_Email
ON Employees(Email);

-- Composite Index: Multiple columns
CREATE NONCLUSTERED INDEX IX_Dept_Salary
ON Employees(DepartmentID, Salary);

-- Index with INCLUDE: Cover index
CREATE NONCLUSTERED INDEX IX_Employee_Include
ON Employees(EmployeeID)
INCLUDE (EmployeeName, Salary);

-- View indexes on table
EXEC sp_helpindex 'Employees';
SELECT * FROM sys.indexes WHERE object_id = OBJECT_ID('Employees');

-- Drop index
DROP INDEX IX_Employee_Name ON Employees;

-- Disable/Rebuild index
ALTER INDEX IX_Employee_Name ON Employees DISABLE;
ALTER INDEX IX_Employee_Name ON Employees REBUILD;
ALTER INDEX ALL ON Employees REORGANIZE;
```

---

### Q27: What is the difference between Clustered and Non-Clustered Index?

| Feature | Clustered | Non-Clustered |
|---------|-----------|---------------|
| **Count per table** | Only 1 | Up to 999 |
| **Physical order** | Determines table order | Separate structure |
| **Unique** | Can be non-unique | Usually unique |
| **Leaf nodes** | Contain data pages | Contain index keys + row locator |
| **Speed** | Faster (table order) | Slower (lookup + navigation) |
| **Primary Key** | Usually clustered | Can be non-clustered |

```sql
-- Clustered Index usually on Primary Key
CREATE CLUSTERED INDEX IX_PK_Employee 
ON Employees(EmployeeID);

-- Non-Clustered for search columns
CREATE NONCLUSTERED INDEX IX_SearchName
ON Employees(EmployeeName);
```

---

### Q28: When and why should we use indexes?

**✅ Create indexes on:**
- Primary and Foreign Keys
- Columns used in WHERE clause frequently
- Columns used in JOIN conditions
- Columns used in ORDER BY or GROUP BY
- Large result set columns (filtered heavily)

**❌ Avoid indexes on:**
- Columns with low cardinality (few unique values: Gender, Status)
- Columns updated frequently (maintenance cost)
- Small tables
- VARCHAR(MAX), TEXT, BLOB columns
- Columns with many NULL values

```sql
-- Good index
CREATE NONCLUSTERED INDEX IX_Employee_DeptID
ON Employees(DepartmentID)  -- Frequently joined
WHERE IsActive = 1;         -- Filtered index

-- Bad index (low cardinality)
CREATE NONCLUSTERED INDEX IX_Gender
ON Employees(Gender);  -- Only M/F, rarely filtered

-- Query using index
SELECT * FROM Employees WHERE DepartmentID = 1;  -- Uses IX_Employee_DeptID
```

---

### Q29: What is query optimization and performance tuning?

**Performance Tuning Techniques:**

```sql
-- 1. Use WHERE instead of filtering in code
SELECT * FROM Employees WHERE Salary > 50000;  -- Good (database filters)
-- vs fetching all and filtering in app (bad)

-- 2. Use indexes effectively
CREATE NONCLUSTERED INDEX IX_Salary ON Employees(Salary);
SELECT * FROM Employees WHERE Salary > 50000;  -- Uses index

-- 3. Avoid SELECT *
SELECT EmployeeID, EmployeeName, Salary FROM Employees;  -- Good
SELECT * FROM Employees;  -- Bad (fetches all columns)

-- 4. Use TOP to limit results
SELECT TOP 100 * FROM Employees ORDER BY Salary DESC;

-- 5. Avoid functions in WHERE clause (prevents index use)
SELECT * FROM Employees WHERE UPPER(Name) = 'JOHN';  -- Index not used
SELECT * FROM Employees WHERE Name = 'John';          -- Index used

-- 6. Use INNER JOIN instead of nested queries
SELECT * FROM Employees e
INNER JOIN Departments d ON e.DepartmentID = d.DepartmentID;

-- 7. Use EXISTS instead of IN for large tables
SELECT * FROM Employees e
WHERE EXISTS (SELECT 1 FROM Orders o WHERE o.EmployeeID = e.EmployeeID);
-- vs
SELECT * FROM Employees WHERE EmployeeID IN (SELECT EmployeeID FROM Orders);

-- 8. Check execution plan
SET STATISTICS TIME ON;
SELECT * FROM Employees WHERE DepartmentID = 1;
SET STATISTICS TIME OFF;
```

---

### Q30: What is an execution plan and how do you read it?

```sql
-- View execution plan
SET STATISTICS IO ON;
SELECT * FROM Employees WHERE DepartmentID = 1;
SET STATISTICS IO OFF;

-- Graphical plan in SSMS
-- Right-click query → Display Estimated Execution Plan (Ctrl+L)

-- Key metrics in execution plan:
-- - Table Scan: Reads all rows (bad) 🔴
-- - Index Seek: Uses index (good) 🟢
-- - Nested Loop: For small result sets
-- - Hash Join: For large result sets
-- - Cost: Percentage of query cost

-- Example analysis:
-- If you see Table Scan on large table → Create index
-- If parallelism is used → Check server resources
-- If spill to tempdb → Increase memory or optimize query
```

---

## <a id="advanced"></a>## 7️⃣ VIEWS, STORED PROCEDURES & FUNCTIONS

### Q31: What is a view and how do you create it?

```sql
-- CREATE VIEW: Virtual table (no physical storage)
CREATE VIEW EmployeeSalaryView AS
SELECT 
    EmployeeID,
    EmployeeName,
    DepartmentID,
    Salary
FROM Employees
WHERE IsActive = 1;

-- Query the view
SELECT * FROM EmployeeSalaryView WHERE Salary > 50000;

-- UPDATE VIEW: Modify underlying table through view
UPDATE EmployeeSalaryView SET Salary = 60000 WHERE EmployeeID = 1;

-- ALTER VIEW: Modify view definition
ALTER VIEW EmployeeSalaryView AS
SELECT 
    EmployeeID,
    EmployeeName,
    Salary,
    Salary * 12 AS AnnualSalary
FROM Employees;

-- DROP VIEW
DROP VIEW EmployeeSalaryView;

-- Indexed View (Materialized view)
CREATE VIEW EmployeeDeptSummary WITH SCHEMABINDING AS
SELECT 
    DepartmentID,
    COUNT(*) AS EmployeeCount,
    AVG(Salary) AS AvgSalary
FROM dbo.Employees
GROUP BY DepartmentID;

CREATE UNIQUE CLUSTERED INDEX IX_DeptSummary
ON EmployeeDeptSummary(DepartmentID);
```

**Benefits of Views:**
- ✅ Security (hide columns/data)
- ✅ Simplify complex queries
- ✅ Provide abstract interface
- ✅ Logical data independence

---

### Q32: What is a stored procedure and how is it different from a query?

```sql
-- CREATE STORED PROCEDURE
CREATE PROCEDURE sp_GetEmployeesByDepartment
    @DepartmentID INT
AS
BEGIN
    SELECT 
        EmployeeID,
        EmployeeName,
        Salary
    FROM Employees
    WHERE DepartmentID = @DepartmentID
    ORDER BY EmployeeName;
END;

-- Execute procedure
EXECUTE sp_GetEmployeesByDepartment @DepartmentID = 1;
-- or
EXEC sp_GetEmployeesByDepartment 1;

-- Procedure with output parameter
CREATE PROCEDURE sp_GetEmployeeCount
    @DepartmentID INT,
    @EmployeeCount INT OUTPUT
AS
BEGIN
    SELECT @EmployeeCount = COUNT(*)
    FROM Employees
    WHERE DepartmentID = @DepartmentID;
END;

-- Call and get output
DECLARE @Count INT;
EXEC sp_GetEmployeeCount @DepartmentID = 1, @EmployeeCount = @Count OUTPUT;
PRINT 'Total employees: ' + CAST(@Count AS VARCHAR);

-- Procedure with return value
CREATE PROCEDURE sp_AddEmployee
    @EmployeeName VARCHAR(100),
    @Salary DECIMAL(10,2)
AS
BEGIN
    INSERT INTO Employees (EmployeeName, Salary)
    VALUES (@EmployeeName, @Salary);
    
    RETURN SCOPE_IDENTITY();  -- Return new EmployeeID
END;

DECLARE @NewID INT;
EXEC @NewID = sp_AddEmployee 'John', 50000;
PRINT 'New employee ID: ' + CAST(@NewID AS VARCHAR);
```

**Query vs Stored Procedure:**

| Query | Stored Procedure |
|-------|------------------|
| Sent to server each time | Pre-compiled, stored in database |
| Network traffic for query text | Only parameters sent |
| No parameters easily | Parameters, loops, conditions |
| Simple queries | Complex business logic |
| Slower | Faster execution |

---

### Q33: What are user-defined functions (UDF) and their types?

```sql
-- SCALAR FUNCTION: Returns single value
CREATE FUNCTION fn_CalculateBonus(@Salary DECIMAL(10,2))
RETURNS DECIMAL(10,2)
AS
BEGIN
    DECLARE @Bonus DECIMAL(10,2);
    SET @Bonus = @Salary * 0.1;  -- 10% bonus
    RETURN @Bonus;
END;

-- Use scalar function
SELECT 
    EmployeeName,
    Salary,
    dbo.fn_CalculateBonus(Salary) AS Bonus
FROM Employees;

-- TABLE-VALUED FUNCTION: Returns table
CREATE FUNCTION fn_GetEmployeesByDept(@DepartmentID INT)
RETURNS TABLE
AS
RETURN (
    SELECT EmployeeID, EmployeeName, Salary
    FROM Employees
    WHERE DepartmentID = @DepartmentID
);

-- Use table-valued function
SELECT * FROM dbo.fn_GetEmployeesByDept(1);

-- MULTI-STATEMENT TABLE-VALUED FUNCTION
CREATE FUNCTION fn_GetHighEarners()
RETURNS @ResultTable TABLE (
    EmployeeID INT,
    EmployeeName VARCHAR(100),
    Salary DECIMAL(10,2)
)
AS
BEGIN
    INSERT INTO @ResultTable
    SELECT EmployeeID, EmployeeName, Salary
    FROM Employees
    WHERE Salary > 100000;
    
    RETURN;
END;

-- Drop function
DROP FUNCTION fn_CalculateBonus;
```

---

### Q34: What are triggers and how do you use them?

```sql
-- Trigger for INSERT
CREATE TRIGGER tr_Employees_Insert
ON Employees
AFTER INSERT
AS
BEGIN
    INSERT INTO Audit_Log (Action, TableName, DateTime)
    SELECT 'INSERT', 'Employees', GETDATE()
    FROM inserted;  -- 'inserted' contains new rows
END;

-- Trigger for UPDATE
CREATE TRIGGER tr_Employees_Update
ON Employees
AFTER UPDATE
AS
BEGIN
    INSERT INTO Audit_Log (Action, OldValue, NewValue, DateTime)
    SELECT 
        'UPDATE',
        CAST(i.Salary AS VARCHAR),
        CAST(d.Salary AS VARCHAR),
        GETDATE()
    FROM inserted i
    INNER JOIN deleted d ON i.EmployeeID = d.EmployeeID
    WHERE i.Salary <> d.Salary;
END;

-- Trigger for DELETE
CREATE TRIGGER tr_Employees_Delete
ON Employees
AFTER DELETE
AS
BEGIN
    INSERT INTO Audit_Log (Action, TableName, DateTime)
    SELECT 'DELETE', 'Employees', GETDATE()
    FROM deleted;
END;

-- INSTEAD OF trigger (execute instead of action)
CREATE TRIGGER tr_PreventDelete
ON Employees
INSTEAD OF DELETE
AS
BEGIN
    PRINT 'Cannot delete employees!';
    ROLLBACK;
END;

-- Disable/Enable trigger
DISABLE TRIGGER tr_Employees_Insert ON Employees;
ENABLE TRIGGER tr_Employees_Insert ON Employees;

-- Drop trigger
DROP TRIGGER tr_Employees_Insert;
```

---

## <a id="transactions"></a>## 8️⃣ TRANSACTIONS & LOCKS

### Q35: What is a transaction and isolation levels?

```sql
-- Transaction basic
BEGIN TRANSACTION;
    INSERT INTO Accounts VALUES (1, 'John', 1000);
    UPDATE Accounts SET Balance = Balance - 100 WHERE AccountID = 1;
COMMIT;

-- Isolation Levels (control concurrency)

-- READ UNCOMMITTED: Dirty reads possible
SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;
BEGIN TRANSACTION;
    SELECT * FROM Accounts;
COMMIT;

-- READ COMMITTED: Prevents dirty reads (default)
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
BEGIN TRANSACTION;
    SELECT * FROM Accounts;
COMMIT;

-- REPEATABLE READ: Prevents dirty and non-repeatable reads
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;
BEGIN TRANSACTION;
    SELECT * FROM Accounts;
COMMIT;

-- SERIALIZABLE: Prevents all anomalies
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
BEGIN TRANSACTION;
    SELECT * FROM Accounts;
COMMIT;

-- SNAPSHOT: Isolation with row versioning
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;
BEGIN TRANSACTION;
    SELECT * FROM Accounts;
COMMIT;
```

---

### Q36: What are locks and deadlocks?

```sql
-- Shared Lock (Read)
SELECT * FROM Employees WITH (NOLOCK);  -- No lock (dirty read allowed)
SELECT * FROM Employees WITH (UPDLOCK); -- Update lock

-- Exclusive Lock (Write)
BEGIN TRANSACTION;
    UPDATE Employees SET Salary = 60000 WHERE EmployeeID = 1;
    -- Table locked, other users can't write
COMMIT;

-- Deadlock example (two transactions blocking each other)
-- Transaction 1:
BEGIN TRANSACTION;
    UPDATE Table1 SET Col1 = 1;
    WAITFOR DELAY '00:00:05';  -- Wait
    UPDATE Table2 SET Col2 = 1;
COMMIT;

-- Transaction 2 (simultaneously):
BEGIN TRANSACTION;
    UPDATE Table2 SET Col2 = 2;
    UPDATE Table1 SET Col1 = 2;
COMMIT;
-- Both wait for each other → Deadlock!

-- Prevent deadlock: Always access tables in same order
BEGIN TRANSACTION;
    UPDATE Table1 SET Col1 = 1;
    UPDATE Table2 SET Col2 = 1;
COMMIT;

-- Handle deadlock
BEGIN TRY
    BEGIN TRANSACTION;
        UPDATE Employees SET Salary = 60000 WHERE EmployeeID = 1;
    COMMIT;
END TRY
BEGIN CATCH
    IF ERROR_NUMBER() = 1205  -- Deadlock error
        PRINT 'Deadlock detected';
    ROLLBACK;
END CATCH;
```

---

## <a id="backup"></a>## 9️⃣ BACKUP & RECOVERY

### Q37: What are types of backups in SQL Server?

```sql
-- FULL BACKUP: Complete database snapshot
BACKUP DATABASE MyDatabase
TO DISK = 'C:\Backups\MyDatabase_Full.bak'
WITH DESCRIPTION = 'Full backup';

-- DIFFERENTIAL BACKUP: Only changes since last full backup
BACKUP DATABASE MyDatabase
TO DISK = 'C:\Backups\MyDatabase_Diff.bak'
WITH DIFFERENTIAL;

-- TRANSACTION LOG BACKUP: Only transaction log
BACKUP LOG MyDatabase
TO DISK = 'C:\Backups\MyDatabase_Log.bak';

-- RESTORE FULL BACKUP
RESTORE DATABASE MyDatabase
FROM DISK = 'C:\Backups\MyDatabase_Full.bak'
WITH REPLACE;

-- RESTORE TO POINT-IN-TIME
RESTORE DATABASE MyDatabase
FROM DISK = 'C:\Backups\MyDatabase_Full.bak'
WITH REPLACE, RECOVERY;

RESTORE LOG MyDatabase
FROM DISK = 'C:\Backups\MyDatabase_Log.bak'
WITH RECOVERY;

-- Schedule backup
-- Use SQL Server Agent (Jobs) to schedule regular backups
```

---

### Q38: What is the difference between Backup and Recovery?

| Backup | Recovery |
|--------|----------|
| Create copy of database | Restore from backup |
| Preventive measure | Corrective measure |
| Regular activity | On-demand activity |
| Multiple types | Multiple strategies |

---

## <a id="scenarios"></a>## 🔟 REAL-WORLD SCENARIOS

### Q39: Design an E-Commerce database schema

```sql
-- Users Table
CREATE TABLE Users (
    UserID INT PRIMARY KEY IDENTITY(1,1),
    UserName VARCHAR(100) NOT NULL,
    Email VARCHAR(100) UNIQUE NOT NULL,
    Phone VARCHAR(15),
    CreatedDate DATETIME DEFAULT GETDATE()
);

-- Products Table
CREATE TABLE Products (
    ProductID INT PRIMARY KEY IDENTITY(1,1),
    ProductName VARCHAR(200) NOT NULL,
    Description TEXT,
    Price DECIMAL(10,2) NOT NULL CHECK (Price > 0),
    Stock INT NOT NULL CHECK (Stock >= 0),
    CategoryID INT FOREIGN KEY REFERENCES Categories(CategoryID)
);

-- Orders Table
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY IDENTITY(1,1),
    UserID INT NOT NULL FOREIGN KEY REFERENCES Users(UserID),
    OrderDate DATETIME DEFAULT GETDATE(),
    TotalAmount DECIMAL(10,2) NOT NULL,
    Status VARCHAR(20) DEFAULT 'Pending'
);

-- OrderItems Table
CREATE TABLE OrderItems (
    OrderItemID INT PRIMARY KEY IDENTITY(1,1),
    OrderID INT NOT NULL FOREIGN KEY REFERENCES Orders(OrderID),
    ProductID INT NOT NULL FOREIGN KEY REFERENCES Products(ProductID),
    Quantity INT NOT NULL CHECK (Quantity > 0),
    UnitPrice DECIMAL(10,2) NOT NULL
);

-- Categories Table
CREATE TABLE Categories (
    CategoryID INT PRIMARY KEY IDENTITY(1,1),
    CategoryName VARCHAR(50) NOT NULL
);

-- Indexes for performance
CREATE NONCLUSTERED INDEX IX_User_Email ON Users(Email);
CREATE NONCLUSTERED INDEX IX_Order_UserID ON Orders(UserID);
CREATE NONCLUSTERED INDEX IX_OrderItems_OrderID ON OrderItems(OrderID);
```

---

### Q40: Write a query to find top 5 best-selling products

```sql
SELECT TOP 5
    p.ProductID,
    p.ProductName,
    SUM(oi.Quantity) AS TotalSold,
    SUM(oi.Quantity * oi.UnitPrice) AS Revenue
FROM Products p
INNER JOIN OrderItems oi ON p.ProductID = oi.ProductID
INNER JOIN Orders o ON oi.OrderID = o.OrderID
WHERE o.Status = 'Completed'
GROUP BY p.ProductID, p.ProductName
ORDER BY TotalSold DESC;
```

---

### Q41: Write a query to find customers who haven't ordered in 30 days

```sql
SELECT 
    u.UserID,
    u.UserName,
    u.Email,
    MAX(o.OrderDate) AS LastOrderDate
FROM Users u
LEFT JOIN Orders o ON u.UserID = o.UserID
GROUP BY u.UserID, u.UserName, u.Email
HAVING MAX(o.OrderDate) < DATEADD(DAY, -30, GETDATE())
   OR MAX(o.OrderDate) IS NULL
ORDER BY LastOrderDate DESC;
```

---

### Q42: Write a query to calculate running total of sales

```sql
SELECT 
    OrderID,
    OrderDate,
    TotalAmount,
    SUM(TotalAmount) OVER (
        ORDER BY OrderID 
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS RunningTotal
FROM Orders
ORDER BY OrderID;
```

---

### Q43: Write a query to find duplicate emails

```sql
SELECT 
    Email,
    COUNT(*) AS Count
FROM Users
GROUP BY Email
HAVING COUNT(*) > 1;

-- Or get all duplicate records
SELECT *
FROM Users
WHERE Email IN (
    SELECT Email FROM Users GROUP BY Email HAVING COUNT(*) > 1
);
```

---

### Q44: Write a query to delete duplicate records

```sql
-- Identify duplicates
WITH DuplicateRecords AS (
    SELECT *,
        ROW_NUMBER() OVER (PARTITION BY Email ORDER BY UserID) AS RowNum
    FROM Users
)
DELETE FROM DuplicateRecords
WHERE RowNum > 1;
```

---

### Q45: Write a query with CTE for hierarchical data

```sql
-- Manager-Employee hierarchy
WITH EmployeeHierarchy AS (
    -- Base: Top-level managers
    SELECT 
        EmployeeID,
        EmployeeName,
        ManagerID,
        0 AS Level
    FROM Employees
    WHERE ManagerID IS NULL
    
    UNION ALL
    
    -- Recursive: Reports under managers
    SELECT 
        e.EmployeeID,
        e.EmployeeName,
        e.ManagerID,
        eh.Level + 1
    FROM Employees e
    INNER JOIN EmployeeHierarchy eh ON e.ManagerID = eh.EmployeeID
)
SELECT 
    REPLICATE('  ', Level) + EmployeeName AS EmployeeHierarchy,
    Level
FROM EmployeeHierarchy
ORDER BY Level, EmployeeName;
```

---

### Q46: How to handle NULL values?

```sql
-- ISNULL: Replace NULL with value
SELECT 
    EmployeeName,
    ISNULL(MiddleName, 'N/A') AS MiddleName
FROM Employees;

-- COALESCE: First non-null value
SELECT 
    COALESCE(Phone, MobilePhone, Email) AS ContactInfo
FROM Users;

-- NULLIF: Return NULL if two values are equal
SELECT 
    EmployeeName,
    NULLIF(Salary, 0) AS Salary
FROM Employees;

-- IS NULL / IS NOT NULL
SELECT * FROM Employees WHERE ManagerID IS NULL;  -- Top-level managers
SELECT * FROM Employees WHERE ManagerID IS NOT NULL;  -- Reports
```

---

### Q47: How to handle dates?

```sql
-- Current date and time
SELECT GETDATE();           -- 2025-05-27 14:30:45.123
SELECT CAST(GETDATE() AS DATE);  -- 2025-05-27
SELECT CAST(GETDATE() AS TIME);  -- 14:30:45

-- Date arithmetic
SELECT DATEADD(DAY, 30, GETDATE());      -- 30 days from today
SELECT DATEADD(MONTH, 1, GETDATE());     -- 1 month from today
SELECT DATEDIFF(DAY, StartDate, EndDate) AS DaysWorked FROM Employees;

-- Date functions
SELECT DAY(GETDATE()) AS Day;            -- 27
SELECT MONTH(GETDATE()) AS Month;        -- 5
SELECT YEAR(GETDATE()) AS Year;          -- 2025
SELECT EOMONTH(GETDATE()) AS EndOfMonth; -- Last day of current month

-- Format date
SELECT FORMAT(GETDATE(), 'dd/MM/yyyy');  -- 27/05/2025
SELECT FORMAT(GETDATE(), 'MMMM dd, yyyy'); -- May 27, 2025
```

---

### Q48: How to concatenate strings?

```sql
-- String concatenation
SELECT 'Hello' + ' ' + 'World';  -- Hello World

-- With NULL (NULL concatenation = NULL)
SELECT 'Hello' + NULL;  -- NULL (problematic!)

-- Use CONCAT (ignores NULL)
SELECT CONCAT('Hello', ' ', NULL, 'World');  -- Hello World

-- Use ISNULL
SELECT 'Hello' + ISNULL(MiddleName, '') + ' ' + 'World';

-- Multiple columns
SELECT 
    CONCAT(FirstName, ' ', LastName) AS FullName,
    CONCAT(Email, ' (', Phone, ')') AS ContactInfo
FROM Employees;
```

---

### Q49: How to find nth highest salary?

```sql
-- 3rd highest salary
SELECT DISTINCT Salary
FROM Employees
ORDER BY Salary DESC
OFFSET 2 ROWS
FETCH NEXT 1 ROW ONLY;

-- Or using subquery
SELECT TOP 1 Salary
FROM (
    SELECT TOP 3 DISTINCT Salary
    FROM Employees
    ORDER BY Salary DESC
) AS TopSalaries
ORDER BY Salary ASC;

-- Using window function
WITH RankedSalaries AS (
    SELECT 
        EmployeeName,
        Salary,
        DENSE_RANK() OVER (ORDER BY Salary DESC) AS SalaryRank
    FROM Employees
)
SELECT * FROM RankedSalaries WHERE SalaryRank = 3;
```

---

### Q50: Common SQL Server issues and solutions

```sql
-- Issue 1: Query too slow
-- Solution: Check execution plan, add indexes

-- Issue 2: Timeout
-- Solution: Add TOP, filter data, use pagination

SELECT TOP 100 * FROM Employees
WHERE DepartmentID = 1
ORDER BY EmployeeID;

-- Issue 3: Deadlock
-- Solution: Use isolation levels, access tables in order

-- Issue 4: Data inconsistency
-- Solution: Use transactions, constraints

BEGIN TRANSACTION;
    UPDATE Accounts SET Balance = Balance - 100;
    UPDATE Accounts SET Balance = Balance + 100;
COMMIT;

-- Issue 5: Memory leak
-- Solution: Close connections, clear result sets

-- Issue 6: Disk space
-- Solution: Archive old data, backup regularly

-- Issue 7: Permissions error
-- Solution: Grant appropriate permissions

GRANT SELECT, INSERT ON Employees TO [username];
```

---

## 🎓 Final Tips for Interview

1. **Practice queries** - Write them without IDE
2. **Understand relationships** - FK, PK, constraints
3. **Know performance** - Indexes, execution plans
4. **Be ready for scenarios** - Design tables, optimize queries
5. **Understand transactions** - ACID, isolation levels
6. **Study best practices** - Naming conventions, optimization

---

## 📚 Additional Resources

- [Microsoft SQL Server Documentation](https://docs.microsoft.com/en-us/sql/)
- [SQL Performance Explained](https://use-the-index-luke.com/)
- [SSMS Tips & Tricks](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)

---

**Good luck with your interviews! 🚀✨**
