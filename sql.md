# SQL

[⬅️ Back to Table of Contents](README.md)

### 51. What is the difference between INNER JOIN, LEFT JOIN, RIGHT JOIN, and FULL JOIN?

**Answer:** These are different types of SQL JOINs that determine how data is combined from multiple tables:

**INNER JOIN:**
- Returns only the rows that have matching values in both tables
- Excludes rows that don't have matches in either table

**LEFT JOIN (LEFT OUTER JOIN):**
- Returns all rows from the left table and matching rows from the right table
- If no match, NULL values are returned for right table columns

**RIGHT JOIN (RIGHT OUTER JOIN):**
- Returns all rows from the right table and matching rows from the left table
- If no match, NULL values are returned for left table columns

**FULL JOIN (FULL OUTER JOIN):**
- Returns all rows from both tables
- If no match, NULL values are returned for the table without the match

```sql
-- Sample tables
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    CustomerName VARCHAR(100)
);

CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE
);

-- INNER JOIN
SELECT c.CustomerName, o.OrderID
FROM Customers c
INNER JOIN Orders o ON c.CustomerID = o.CustomerID;
-- Returns only customers who have orders

-- LEFT JOIN
SELECT c.CustomerName, o.OrderID
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID;
-- Returns all customers, even those without orders

-- RIGHT JOIN
SELECT c.CustomerName, o.OrderID
FROM Customers c
RIGHT JOIN Orders o ON c.CustomerID = o.CustomerID;
-- Returns all orders, even those without matching customers

-- FULL JOIN
SELECT c.CustomerName, o.OrderID
FROM Customers c
FULL JOIN Orders o ON c.CustomerID = o.CustomerID;
-- Returns all customers and all orders
```

### 52. What is a primary key and how does it differ from a unique key?

**Answer:** Both primary keys and unique keys enforce uniqueness, but they have different purposes and characteristics:

**Primary Key:**
- Uniquely identifies each row in a table
- Cannot contain NULL values
- Only one primary key per table
- Automatically creates a clustered index (in most databases)
- Used as a reference in foreign key relationships

**Unique Key:**
- Ensures uniqueness but allows NULL values
- Multiple unique keys can exist per table
- Does not automatically create a clustered index
- Cannot be used as a foreign key reference

```sql
CREATE TABLE Users (
    UserID INT PRIMARY KEY,           -- Primary key
    Email VARCHAR(100) UNIQUE,        -- Unique key
    Username VARCHAR(50) UNIQUE,      -- Another unique key
    PhoneNumber VARCHAR(20) UNIQUE    -- Another unique key
);

-- Primary key cannot be NULL
INSERT INTO Users (UserID, Email) VALUES (1, 'john@example.com'); -- OK
INSERT INTO Users (Email) VALUES ('jane@example.com'); -- Error: UserID cannot be NULL

-- Unique keys can be NULL
INSERT INTO Users (UserID, Email) VALUES (2, NULL); -- OK
INSERT INTO Users (UserID, Email) VALUES (3, NULL); -- OK (NULL values don't violate uniqueness)
```

### 53. What are foreign keys and how do they enforce referential integrity?

**Answer:** Foreign keys are columns that reference the primary key of another table, establishing relationships between tables and enforcing referential integrity.

**Referential Integrity Rules:**
- You cannot insert a record with a foreign key value that doesn't exist in the referenced table
- You cannot delete a record from the referenced table if it's being referenced by a foreign key (unless CASCADE is specified)
- You cannot update a primary key value if it's being referenced by a foreign key

```sql
CREATE TABLE Departments (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(100)
);

CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    DepartmentID INT,
    FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID)
);

-- This will fail if DepartmentID 999 doesn't exist in Departments
INSERT INTO Employees (EmployeeID, FirstName, LastName, DepartmentID)
VALUES (1, 'John', 'Doe', 999);

-- This will fail if there are employees in Department 1
DELETE FROM Departments WHERE DepartmentID = 1;

-- To allow cascading deletes
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    DepartmentID INT,
    FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID)
    ON DELETE CASCADE -- Deletes employees when department is deleted
);
```

### 54. Explain normalization and list the different normal forms.

**Answer:** Normalization is a database design technique that organizes data to reduce redundancy and improve data integrity. It involves decomposing tables into smaller, more manageable tables.

**First Normal Form (1NF):**
- Each column contains atomic values (no arrays or lists)
- Each row is unique
- No repeating groups

**Second Normal Form (2NF):**
- Must be in 1NF
- All non-key attributes must be fully dependent on the primary key
- No partial dependencies

**Third Normal Form (3NF):**
- Must be in 2NF
- No transitive dependencies (non-key attributes don't depend on other non-key attributes)

**Boyce-Codd Normal Form (BCNF):**
- Must be in 3NF
- Every determinant must be a candidate key

```sql
-- Before normalization (not in 1NF)
CREATE TABLE Orders (
    OrderID INT,
    CustomerName VARCHAR(100),
    Products VARCHAR(500) -- Contains "Product1,Product2,Product3"
);

-- After 1NF
CREATE TABLE Orders (
    OrderID INT,
    CustomerName VARCHAR(100)
);

CREATE TABLE OrderItems (
    OrderID INT,
    ProductID INT,
    Quantity INT
);

-- After 2NF (separate customer table)
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    CustomerName VARCHAR(100)
);

CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);

-- After 3NF (separate product table)
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(100),
    Price DECIMAL(10,2)
);

CREATE TABLE OrderItems (
    OrderID INT,
    ProductID INT,
    Quantity INT,
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID),
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
);
```

### 55. What is a clustered index vs a non-clustered index?

**Answer:** Indexes improve query performance by providing faster data access. There are two main types:

**Clustered Index:**
- Determines the physical order of data in the table
- Only one clustered index per table
- Usually created automatically on the primary key
- Data is stored in the same order as the index
- Faster for range queries and sorting

**Non-Clustered Index:**
- Separate structure that points to the actual data
- Multiple non-clustered indexes per table
- Contains index key values and row locators
- Slower than clustered indexes but still faster than table scans

```sql
-- Clustered index (usually on primary key)
CREATE TABLE Users (
    UserID INT PRIMARY KEY, -- Automatically creates clustered index
    Username VARCHAR(50),
    Email VARCHAR(100)
);

-- Non-clustered index
CREATE INDEX IX_Users_Email ON Users(Email);

-- Composite non-clustered index
CREATE INDEX IX_Users_Username_Email ON Users(Username, Email);

-- Unique non-clustered index
CREATE UNIQUE INDEX IX_Users_Username ON Users(Username);
```

**Performance Considerations:**
- Clustered indexes are best for columns used in ORDER BY, GROUP BY, and range queries
- Non-clustered indexes are good for columns used in WHERE clauses
- Too many indexes can slow down INSERT, UPDATE, and DELETE operations

### 56. What are transactions in SQL and what are ACID properties?

**Answer:** Transactions are groups of SQL statements that are executed as a single unit. They ensure data consistency and integrity.

**ACID Properties:**

**Atomicity:** All operations in a transaction succeed or all fail
**Consistency:** Database remains in a valid state before and after transaction
**Isolation:** Concurrent transactions don't interfere with each other
**Durability:** Committed transactions are permanent

```sql
-- Transaction example
BEGIN TRANSACTION;

BEGIN TRY
    -- Debit from account A
    UPDATE Accounts 
    SET Balance = Balance - 100 
    WHERE AccountID = 1;
    
    -- Credit to account B
    UPDATE Accounts 
    SET Balance = Balance + 100 
    WHERE AccountID = 2;
    
    COMMIT TRANSACTION;
    PRINT 'Transaction completed successfully';
END TRY
BEGIN CATCH
    ROLLBACK TRANSACTION;
    PRINT 'Transaction failed and rolled back';
    PRINT ERROR_MESSAGE();
END CATCH
```

**Transaction Isolation Levels:**
- **READ UNCOMMITTED:** Lowest isolation, allows dirty reads
- **READ COMMITTED:** Default level, prevents dirty reads
- **REPEATABLE READ:** Prevents non-repeatable reads
- **SERIALIZABLE:** Highest isolation, prevents phantom reads

```sql
-- Set isolation level
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;

BEGIN TRANSACTION;
-- Transaction code here
COMMIT TRANSACTION;
```

### 57. What is the difference between DELETE, TRUNCATE, and DROP?

**Answer:** These are different ways to remove data from a database:

**DELETE:**
- Removes specific rows based on WHERE clause
- Can be rolled back (if within a transaction)
- Triggers are fired
- Slower for large datasets
- Maintains auto-increment counters

**TRUNCATE:**
- Removes all rows from a table
- Cannot be rolled back
- Triggers are not fired
- Faster than DELETE
- Resets auto-increment counters
- Requires higher permissions

**DROP:**
- Removes the entire table structure and data
- Cannot be rolled back
- All indexes and constraints are also removed
- Requires highest permissions

```sql
-- DELETE examples
DELETE FROM Users WHERE UserID = 1; -- Delete specific row
DELETE FROM Users WHERE LastLogin < '2023-01-01'; -- Delete based on condition
DELETE FROM Users; -- Delete all rows (but table structure remains)

-- TRUNCATE example
TRUNCATE TABLE Users; -- Remove all rows, reset auto-increment

-- DROP example
DROP TABLE Users; -- Remove entire table

-- Comparison
-- DELETE: Logged, can be rolled back, slower
-- TRUNCATE: Minimal logging, cannot be rolled back, faster
-- DROP: Removes everything, cannot be rolled back, fastest
```

### 58. What are window functions in SQL and when would you use them?

**Answer:** Window functions perform calculations across a set of rows related to the current row, without grouping the result set.

**Common Window Functions:**
- **ROW_NUMBER():** Assigns unique sequential numbers
- **RANK():** Assigns rank with gaps for ties
- **DENSE_RANK():** Assigns rank without gaps for ties
- **LAG()/LEAD():** Access previous/next row values
- **SUM(), AVG(), COUNT():** Aggregate functions over windows

```sql
-- Sample data
CREATE TABLE Sales (
    ProductID INT,
    SaleDate DATE,
    Amount DECIMAL(10,2)
);

-- ROW_NUMBER() - rank products by sales amount
SELECT 
    ProductID,
    Amount,
    ROW_NUMBER() OVER (ORDER BY Amount DESC) as RowNum
FROM Sales;

-- RANK() vs DENSE_RANK()
SELECT 
    ProductID,
    Amount,
    RANK() OVER (ORDER BY Amount DESC) as Rank,
    DENSE_RANK() OVER (ORDER BY Amount DESC) as DenseRank
FROM Sales;

-- LAG() - compare with previous row
SELECT 
    ProductID,
    SaleDate,
    Amount,
    LAG(Amount, 1) OVER (ORDER BY SaleDate) as PreviousAmount,
    Amount - LAG(Amount, 1) OVER (ORDER BY SaleDate) as Difference
FROM Sales;

-- Running total
SELECT 
    ProductID,
    SaleDate,
    Amount,
    SUM(Amount) OVER (ORDER BY SaleDate) as RunningTotal
FROM Sales;

-- Partition by product
SELECT 
    ProductID,
    SaleDate,
    Amount,
    ROW_NUMBER() OVER (PARTITION BY ProductID ORDER BY SaleDate) as ProductRowNum
FROM Sales;
```

### 59. How does a Common Table Expression (CTE) work and how is it different from a subquery?

**Answer:** CTEs are temporary named result sets that exist only within the scope of a single SQL statement. They provide better readability and can be referenced multiple times.

**CTE Syntax:**
```sql
WITH CTE_Name AS (
    SELECT column1, column2
    FROM table1
    WHERE condition
)
SELECT * FROM CTE_Name;
```

**CTE vs Subquery:**
- CTEs are more readable and can be referenced multiple times
- Subqueries are embedded within the main query
- CTEs can be recursive (for hierarchical data)

```sql
-- Using CTE
WITH HighValueOrders AS (
    SELECT OrderID, CustomerID, TotalAmount
    FROM Orders
    WHERE TotalAmount > 1000
),
CustomerSummary AS (
    SELECT 
        h.CustomerID,
        COUNT(*) as OrderCount,
        SUM(h.TotalAmount) as TotalSpent
    FROM HighValueOrders h
    GROUP BY h.CustomerID
)
SELECT 
    c.CustomerName,
    cs.OrderCount,
    cs.TotalSpent
FROM CustomerSummary cs
JOIN Customers c ON cs.CustomerID = c.CustomerID;

-- Equivalent subquery
SELECT 
    c.CustomerName,
    (SELECT COUNT(*) FROM Orders o WHERE o.CustomerID = c.CustomerID AND o.TotalAmount > 1000) as OrderCount,
    (SELECT SUM(o.TotalAmount) FROM Orders o WHERE o.CustomerID = c.CustomerID AND o.TotalAmount > 1000) as TotalSpent
FROM Customers c
WHERE EXISTS (SELECT 1 FROM Orders o WHERE o.CustomerID = c.CustomerID AND o.TotalAmount > 1000);

-- Recursive CTE (for hierarchical data)
WITH EmployeeHierarchy AS (
    -- Anchor member
    SELECT EmployeeID, Name, ManagerID, 0 as Level
    FROM Employees
    WHERE ManagerID IS NULL
    
    UNION ALL
    
    -- Recursive member
    SELECT e.EmployeeID, e.Name, e.ManagerID, eh.Level + 1
    FROM Employees e
    JOIN EmployeeHierarchy eh ON e.ManagerID = eh.EmployeeID
)
SELECT * FROM EmployeeHierarchy;
```

### 60. What are the advantages and disadvantages of using stored procedures?

**Answer:** Stored procedures are precompiled SQL statements stored in the database.

**Advantages:**
- **Performance:** Precompiled and cached
- **Security:** Can control access to data
- **Maintainability:** Centralized business logic
- **Network traffic:** Reduced by sending procedure name instead of SQL
- **Consistency:** Ensures same logic across applications

**Disadvantages:**
- **Vendor lock-in:** Database-specific syntax
- **Testing:** Harder to test than application code
- **Version control:** Not as well integrated as application code
- **Debugging:** Limited debugging capabilities
- **Scalability:** Can become bottlenecks

```sql
-- Simple stored procedure
CREATE PROCEDURE GetCustomerOrders
    @CustomerID INT
AS
BEGIN
    SELECT o.OrderID, o.OrderDate, o.TotalAmount
    FROM Orders o
    WHERE o.CustomerID = @CustomerID
    ORDER BY o.OrderDate DESC;
END;

-- Execute stored procedure
EXEC GetCustomerOrders @CustomerID = 1;

-- Stored procedure with output parameter
CREATE PROCEDURE GetCustomerInfo
    @CustomerID INT,
    @CustomerName VARCHAR(100) OUTPUT,
    @OrderCount INT OUTPUT
AS
BEGIN
    SELECT @CustomerName = CustomerName
    FROM Customers
    WHERE CustomerID = @CustomerID;
    
    SELECT @OrderCount = COUNT(*)
    FROM Orders
    WHERE CustomerID = @CustomerID;
END;

-- Execute with output parameters
DECLARE @Name VARCHAR(100), @Count INT;
EXEC GetCustomerInfo @CustomerID = 1, @CustomerName = @Name OUTPUT, @OrderCount = @Count OUTPUT;
PRINT 'Customer: ' + @Name + ', Orders: ' + CAST(@Count AS VARCHAR);
``` 