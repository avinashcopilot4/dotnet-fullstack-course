# 📝 SQL SELECT Practice Questions - 25 Interview-Ready Questions
## E-Commerce Database | Easy → Hard | All Important Topics

---

## 📖 Table of Contents
1. [Difficulty: EASY (5 Questions)](#easy)
2. [Difficulty: MEDIUM (10 Questions)](#medium)
3. [Difficulty: HARD (7 Questions)](#hard)
4. [Difficulty: EXPERT (3 Questions)](#expert)
5. [Solutions & Explanations](#solutions)
6. [Interview Tips](#tips)

---

## ⚡ Quick Setup (Run First)

```sql
-- Run all CREATE and INSERT statements from Capstone_Project_ECommerce_Database.md
-- Before attempting these questions
```

---

## <a id="easy"></a>🟢 EASY - Basic SELECT (5 Questions)

### Q1: Select All Users
**Topic: Basic SELECT, SELECT ***

Display all users with all their information.

<details>
<summary>Click to see Question Details</summary>

**Expected Output Columns:** UserID, UserName, Email, Phone, City

**Sample Output:**
```
UserID | UserName    | Email             | Phone      | City
1      | Raj Kumar   | raj@email.com     | 9876543210 | Delhi
2      | Priya Singh | priya@email.com   | 9876543211 | Mumbai
```

</details>

<details>
<summary>Click for Answer</summary>

```sql
SELECT * FROM Users;
```

**OR (More specific):**
```sql
SELECT UserID, UserName, Email, Phone, City FROM Users;
```

</details>

---

### Q2: Select Specific Columns
**Topic: Column Selection, Aliases**

Display only the UserName and Email of all customers, rename Email column as "Contact Email".

<details>
<summary>Click for Answer</summary>

```sql
SELECT 
    UserName,
    Email AS 'Contact Email'
FROM Users;
```

</details>

---

### Q3: Select All Products with Price
**Topic: SELECT, WHERE with Simple Condition**

Display all electronics products (products where category = 'Electronics').

<details>
<summary>Click for Answer</summary>

```sql
SELECT 
    ProductID,
    ProductName,
    Category,
    Price,
    Stock
FROM Products
WHERE Category = 'Electronics';
```

</details>

---

### Q4: Filter with Comparison Operator
**Topic: WHERE with >, <, >=, <=**

Find all products with price greater than 50000.

<details>
<summary>Click for Answer</summary>

```sql
SELECT 
    ProductID,
    ProductName,
    Price,
    Stock
FROM Products
WHERE Price > 50000
ORDER BY Price DESC;
```

</details>

---

### Q5: Simple Sorting
**Topic: ORDER BY ASC/DESC**

List all orders sorted by TotalAmount in descending order (highest first).

<details>
<summary>Click for Answer</summary>

```sql
SELECT 
    OrderID,
    UserID,
    OrderDate,
    TotalAmount,
    Status
FROM Orders
ORDER BY TotalAmount DESC;
```

</details>

---

## <a id="medium"></a>🟡 MEDIUM - JOINs & Filtering (10 Questions)

### Q6: Simple INNER JOIN
**Topic: INNER JOIN, Table Relationships**

Display each order with the customer's name and city.

<details>
<summary>Click for Answer</summary>

```sql
SELECT 
    o.OrderID,
    u.UserName,
    u.City,
    o.OrderDate,
    o.TotalAmount,
    o.Status
FROM Orders o
INNER JOIN Users u ON o.UserID = u.UserID
ORDER BY o.OrderID;
```

**Explanation:**
- `o` = alias for Orders table
- `u` = alias for Users table
- `INNER JOIN` = only matching rows
- `ON o.UserID = u.UserID` = join condition (FK to PK)

</details>

---

### Q7: Multiple JOINs
**Topic: Multiple JOINs, 3+ Table Join**

Display each order item with: OrderID, Customer Name, Product Name, and Price.

<details>
<summary>Click for Answer</summary>

```sql
SELECT 
    oi.OrderItemID,
    o.OrderID,
    u.UserName,
    p.ProductName,
    oi.Quantity,
    oi.UnitPrice,
    (oi.Quantity * oi.UnitPrice) AS 'Line Total'
FROM OrderItems oi
INNER JOIN Orders o ON oi.OrderID = o.OrderID
INNER JOIN Users u ON o.UserID = u.UserID
INNER JOIN Products p ON oi.ProductID = p.ProductID
ORDER BY o.OrderID;
```

**Key Points:**
- **4-table JOIN** (OrderItems, Orders, Users, Products)
- Calculation: `Quantity * UnitPrice = Line Total`
- Alias names make code readable

</details>

---

### Q8: LEFT JOIN to Find Missing Data
**Topic: LEFT JOIN, Finding NULL values**

Show all users and their orders. Include users who haven't placed any orders.

<details>
<summary>Click for Answer</summary>

```sql
SELECT 
    u.UserID,
    u.UserName,
    u.City,
    o.OrderID,
    o.OrderDate,
    o.TotalAmount
FROM Users u
LEFT JOIN Orders o ON u.UserID = o.UserID
ORDER BY u.UserID;
```

**Explanation:**
- `LEFT JOIN` = All users + matching orders
- Users with no orders will have NULL in order columns
- Perfect for finding customers who never ordered

</details>

---

### Q9: WHERE with AND/OR
**Topic: Multiple Conditions, Logical Operators**

Find all orders with status "Delivered" AND TotalAmount > 50000.

<details>
<summary>Click for Answer</summary>

```sql
SELECT 
    OrderID,
    UserID,
    OrderDate,
    TotalAmount,
    Status
FROM Orders
WHERE Status = 'Delivered' AND TotalAmount > 50000
ORDER BY TotalAmount DESC;
```

**Variations:**
```sql
-- OR condition
SELECT * FROM Orders 
WHERE Status = 'Delivered' OR Status = 'Shipped';

-- Better: Use IN
SELECT * FROM Orders 
WHERE Status IN ('Delivered', 'Shipped');
```

</details>

---

### Q10: LIKE for Pattern Matching
**Topic: LIKE, Wildcards (%, _)**

Find all customers whose name starts with 'R' or contains 'Kumar'.

<details>
<summary>Click for Answer</summary>

```sql
-- Names starting with R
SELECT * FROM Users 
WHERE UserName LIKE 'R%';

-- Names containing Kumar
SELECT * FROM Users 
WHERE UserName LIKE '%Kumar%';

-- Both conditions
SELECT * FROM Users 
WHERE UserName LIKE 'R%' OR UserName LIKE '%Kumar%';
```

**LIKE Patterns:**
- `'R%'` = Starts with R
- `'%Kumar%'` = Contains Kumar anywhere
- `'%Singh'` = Ends with Singh
- `'_raj_'` = Exactly 5 chars with raj in middle

</details>

---

### Q11: BETWEEN Range Query
**Topic: BETWEEN Operator, Range Filtering**

Find all products with price between 10000 and 50000.

<details>
<summary>Click for Answer</summary>

```sql
SELECT 
    ProductID,
    ProductName,
    Category,
    Price,
    Stock
FROM Products
WHERE Price BETWEEN 10000 AND 50000
ORDER BY Price;
```

**Equivalent (but more verbose):**
```sql
SELECT * FROM Products
WHERE Price >= 10000 AND Price <= 50000;
```

</details>

---

### Q12: IN Operator with Multiple Values
**Topic: IN Operator, Multiple Values**

Show all products in categories 'Electronics' or 'Fashion'.

<details>
<summary>Click for Answer</summary>

```sql
SELECT 
    ProductID,
    ProductName,
    Category,
    Price
FROM Products
WHERE Category IN ('Electronics', 'Fashion')
ORDER BY Category, Price;
```

**Equivalent (but longer):**
```sql
SELECT * FROM Products
WHERE Category = 'Electronics' OR Category = 'Fashion';
```

</details>

---

### Q13: NULL Checking
**Topic: IS NULL, IS NOT NULL**

Find all products with stock information (Stock is NOT NULL).

<details>
<summary>Click for Answer</summary>

```sql
-- Products WITH stock
SELECT * FROM Products
WHERE Stock IS NOT NULL;

-- Products WITHOUT stock (empty/unknown)
SELECT * FROM Products
WHERE Stock IS NULL;
```

**Important:** 
- Use `IS NULL` or `IS NOT NULL`
- ❌ DON'T use `= NULL` or `!= NULL` (won't work!)

</details>

---

### Q14: Calculated Columns
**Topic: Expressions, Calculations, Aliases**

For each product, show: ProductName, Price, and Price with 10% discount.

<details>
<summary>Click for Answer</summary>

```sql
SELECT 
    ProductName,
    Price,
    (Price * 0.9) AS 'Price After 10% Discount',
    (Price - Price * 0.1) AS 'Alternative Calculation'
FROM Products
ORDER BY Price DESC;
```

**Operations:**
- `Price * 0.9` = 90% of price (10% off)
- `Price * 1.1` = 110% of price (10% markup)
- Can use +, -, *, / operators

</details>

---

### Q15: DISTINCT - Remove Duplicates
**Topic: DISTINCT, Unique Values**

Show all unique cities where customers are located.

<details>
<summary>Click for Answer</summary>

```sql
SELECT DISTINCT City
FROM Users
ORDER BY City;
```

**Without DISTINCT (shows duplicates):**
```sql
SELECT City FROM Users;
-- Would show Delhi, Mumbai, Bangalore, etc. (might repeat)
```

</details>

---

## <a id="hard"></a>🔴 HARD - Aggregates & GROUP BY (7 Questions)

### Q16: COUNT Aggregate Function
**Topic: COUNT, Aggregate Functions**

Count total number of orders and total number of customers.

<details>
<summary>Click for Answer</summary>

```sql
-- Total orders
SELECT COUNT(*) AS 'Total Orders'
FROM Orders;

-- Total customers
SELECT COUNT(DISTINCT UserID) AS 'Total Customers'
FROM Users;

-- Both together
SELECT 
    (SELECT COUNT(*) FROM Orders) AS 'Total Orders',
    (SELECT COUNT(*) FROM Users) AS 'Total Customers';
```

</details>

---

### Q17: SUM - Calculate Totals
**Topic: SUM, Aggregate Functions**

Calculate total revenue from all orders.

<details>
<summary>Click for Answer</summary>

```sql
SELECT 
    SUM(TotalAmount) AS 'Total Revenue',
    AVG(TotalAmount) AS 'Average Order Value',
    MIN(TotalAmount) AS 'Minimum Order',
    MAX(TotalAmount) AS 'Maximum Order'
FROM Orders;
```

**Common Aggregates:**
- `COUNT()` = Number of rows
- `SUM()` = Total of column
- `AVG()` = Average value
- `MIN()` = Smallest value
- `MAX()` = Largest value

</details>

---

### Q18: GROUP BY - Aggregates Per Group
**Topic: GROUP BY, GROUP BY with Aggregate**

Show total revenue per customer.

<details>
<summary>Click for Answer</summary>

```sql
SELECT 
    u.UserName,
    COUNT(o.OrderID) AS 'Total Orders',
    SUM(o.TotalAmount) AS 'Total Spent'
FROM Users u
LEFT JOIN Orders o ON u.UserID = o.UserID
GROUP BY u.UserID, u.UserName
ORDER BY 'Total Spent' DESC;
```

**Important:**
- When using `GROUP BY`, SELECT only grouped columns or aggregates
- ✅ `SELECT UserID, COUNT(*) ... GROUP BY UserID;`
- ❌ `SELECT UserID, UserName, COUNT(*) ... GROUP BY UserID;` (ERROR!)

</details>

---

### Q19: GROUP BY with Multiple Columns
**Topic: GROUP BY Multiple Columns, Aggregates**

Show total orders and total revenue per order status.

<details>
<summary>Click for Answer</summary>

```sql
SELECT 
    Status,
    COUNT(*) AS 'Number of Orders',
    SUM(TotalAmount) AS 'Total Revenue',
    AVG(TotalAmount) AS 'Average Order Value'
FROM Orders
GROUP BY Status
ORDER BY 'Total Revenue' DESC;
```

**Sample Output:**
```
Status    | Number of Orders | Total Revenue | Average Order Value
Delivered | 12               | 1,500,000     | 125,000
Shipped   | 4                | 500,000       | 125,000
Pending   | 4                | 400,000       | 100,000
```

</details>

---

### Q20: HAVING - Filter Groups
**Topic: HAVING Clause, Filtering Groups**

Find customers who have spent more than 100,000 in total.

<details>
<summary>Click for Answer</summary>

```sql
SELECT 
    u.UserName,
    COUNT(o.OrderID) AS 'Total Orders',
    SUM(o.TotalAmount) AS 'Total Spent'
FROM Users u
LEFT JOIN Orders o ON u.UserID = o.UserID
GROUP BY u.UserID, u.UserName
HAVING SUM(o.TotalAmount) > 100000
ORDER BY 'Total Spent' DESC;
```

**WHERE vs HAVING:**
- `WHERE` = Filter ROWS before grouping
- `HAVING` = Filter GROUPS after grouping

```sql
-- WHERE: Filter individual orders > 50000
SELECT * FROM Orders WHERE TotalAmount > 50000;

-- HAVING: Filter grouped totals > 100000
SELECT UserID, SUM(TotalAmount)
FROM Orders
GROUP BY UserID
HAVING SUM(TotalAmount) > 100000;
```

</details>

---

### Q21: Top N Products by Sales
**Topic: GROUP BY, ORDER BY, TOP, Aggregates**

Find top 5 best-selling products by quantity.

<details>
<summary>Click for Answer</summary>

```sql
SELECT TOP 5
    p.ProductID,
    p.ProductName,
    p.Category,
    SUM(oi.Quantity) AS 'Total Sold',
    SUM(oi.Quantity * oi.UnitPrice) AS 'Revenue'
FROM Products p
INNER JOIN OrderItems oi ON p.ProductID = oi.ProductID
GROUP BY p.ProductID, p.ProductName, p.Category
ORDER BY 'Total Sold' DESC;
```

**SQL Server Syntax:**
- `TOP 5` = Show only first 5 rows
- Other DBs use `LIMIT 5` (MySQL) or `FETCH FIRST 5 ROWS` (PostgreSQL)

</details>

---

### Q22: Complex GROUP BY with JOINs
**Topic: Multiple JOINs, GROUP BY, Multiple Aggregates**

Show products sold per category with total quantity and revenue.

<details>
<summary>Click for Answer</summary>

```sql
SELECT 
    p.Category,
    COUNT(DISTINCT p.ProductID) AS 'Number of Products',
    SUM(oi.Quantity) AS 'Total Quantity Sold',
    SUM(oi.Quantity * oi.UnitPrice) AS 'Total Revenue',
    AVG(p.Price) AS 'Average Price'
FROM Products p
INNER JOIN OrderItems oi ON p.ProductID = oi.ProductID
GROUP BY p.Category
ORDER BY 'Total Revenue' DESC;
```

**Sample Output:**
```
Category    | Products | Qty | Revenue  | Avg Price
Electronics | 12       | 25  | 1,200,000| 50,000
Fashion     | 10       | 18  | 300,000  | 10,000
```

</details>

---

## <a id="expert"></a>🚀 EXPERT - Complex & Real-World (3 Questions)

### Q23: Subquery in WHERE Clause
**Topic: Subqueries, Nested Queries**

Find all orders with total amount greater than the average order value.

<details>
<summary>Click for Answer</summary>

```sql
SELECT 
    OrderID,
    UserID,
    TotalAmount,
    Status
FROM Orders
WHERE TotalAmount > (SELECT AVG(TotalAmount) FROM Orders)
ORDER BY TotalAmount DESC;
```

**Explanation:**
- Subquery: `(SELECT AVG(TotalAmount) FROM Orders)` = calculates average first
- Outer query: Uses that average to filter orders
- Executes from inside out

</details>

---

### Q24: Subquery in SELECT (Derived Column)
**Topic: Subqueries in SELECT, Correlation**

For each customer, show their orders with percentage of total revenue.

<details>
<summary>Click for Answer</summary>

```sql
SELECT 
    u.UserName,
    o.OrderID,
    o.TotalAmount,
    (SELECT SUM(TotalAmount) FROM Orders WHERE UserID = u.UserID) AS 'Customer Total',
    ROUND((o.TotalAmount * 100.0 / 
        (SELECT SUM(TotalAmount) FROM Orders WHERE UserID = u.UserID)), 2) AS 'Percentage'
FROM Orders o
INNER JOIN Users u ON o.UserID = u.UserID
ORDER BY u.UserID, o.TotalAmount DESC;
```

**Complex but Real-World!**
- Shows each order's percentage of that customer's total spending
- Uses ROUND() for decimal places

</details>

---

### Q25: Window Functions / Ranking
**Topic: Window Functions (Advanced), ROW_NUMBER, RANK**

Rank products by revenue within each category.

<details>
<summary>Click for Answer</summary>

```sql
SELECT 
    p.Category,
    p.ProductName,
    SUM(oi.Quantity * oi.UnitPrice) AS 'Revenue',
    ROW_NUMBER() OVER (PARTITION BY p.Category ORDER BY SUM(oi.Quantity * oi.UnitPrice) DESC) AS 'Rank in Category'
FROM Products p
INNER JOIN OrderItems oi ON p.ProductID = oi.ProductID
GROUP BY p.Category, p.ProductID, p.ProductName
ORDER BY p.Category, 'Rank in Category';
```

**Window Functions Concepts:**
- `ROW_NUMBER()` = Sequential number (1, 2, 3...)
- `PARTITION BY` = Group by category
- `ORDER BY` = Sort within each partition
- Very useful for ranking, moving averages, etc.

</details>

---

## <a id="solutions"></a>📚 Solutions & Explanations

### Summary of Key SQL Concepts Covered:

| Topic | Questions | Key Points |
|-------|-----------|-----------|
| **Basic SELECT** | Q1-Q5 | SELECT *, columns, WHERE, ORDER BY |
| **JOINs** | Q6-Q8 | INNER JOIN, Multiple JOINs, LEFT JOIN |
| **WHERE Conditions** | Q9-Q15 | AND/OR, LIKE, BETWEEN, IN, NULL, Calculations |
| **Aggregates** | Q16-Q17 | COUNT, SUM, AVG, MIN, MAX |
| **GROUP BY** | Q18-Q22 | GROUP BY, HAVING, Multiple columns |
| **Advanced** | Q23-Q25 | Subqueries, Window Functions |

---

## <a id="tips"></a>💡 Interview Tips

### Common Interview Questions About These Topics:

#### Q: Difference between WHERE and HAVING?
```
WHERE: Filters INDIVIDUAL ROWS before grouping
HAVING: Filters GROUPS after grouping
```

#### Q: Why use LEFT JOIN over INNER JOIN?
```
INNER JOIN: Only matching rows
LEFT JOIN: All left table rows + matching right rows
Use LEFT JOIN when you need to find missing/unmatched data
```

#### Q: What's wrong with this?
```sql
-- ❌ WRONG
SELECT UserID, UserName, COUNT(*) 
FROM Orders 
GROUP BY UserID;  -- UserName not in GROUP BY!

-- ✅ CORRECT
SELECT UserID, UserName, COUNT(*)
FROM Users u
INNER JOIN Orders o ON u.UserID = o.UserID
GROUP BY u.UserID, u.UserName;
```

#### Q: Performance Tip
```sql
-- ❌ SLOW: Subquery in SELECT (runs for each row)
SELECT (SELECT COUNT(*) FROM Orders) AS Total FROM Users;

-- ✅ FASTER: Subquery once
SELECT COUNT(*) AS Total FROM Orders;
```

### Interview Do's & Don'ts:

✅ **DO:**
- Always use table aliases for clarity
- Use meaningful column names (AS 'alias')
- Test WHERE clause with SELECT first before DELETE/UPDATE
- Use proper JOIN conditions
- Comment your complex queries

❌ **DON'T:**
- Use `SELECT *` in production code
- Use `= NULL` or `!= NULL` (use IS NULL)
- Forget to include all non-aggregated columns in GROUP BY
- Use INNER JOIN when LEFT JOIN is needed
- Assume column order in SELECT matches ORDER BY position

---

## 🎓 Practice Tips

### 1. **Start with Easy Questions**
- Build confidence with basic SELECT
- Understand table structure first

### 2. **Practice JOINs Extensively**
- Most interview questions use JOINs
- Understand 1-to-Many and Many-to-Many relationships
- Practice LEFT JOIN for finding missing data

### 3. **Master GROUP BY**
- Very common in real-world queries
- Understand difference between WHERE and HAVING
- Practice with multiple columns

### 4. **Understand Execution Order**
```
FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY
```

### 5. **Test Your Queries**
- Run each query against the E-Commerce database
- Verify results make sense
- Modify queries to understand changes

---

## 🚀 Next Steps

After mastering these 25 questions:
1. ✅ Try writing queries for business problems
2. ✅ Optimize queries for performance
3. ✅ Learn about indexes and query plans
4. ✅ Practice complex joins with 5+ tables
5. ✅ Learn about stored procedures and views

---

## 📊 Difficulty Distribution

| Difficulty | Count | Focus Area |
|-----------|-------|-----------|
| **Easy** | 5 | Basics |
| **Medium** | 10 | JOINs & Filtering |
| **Hard** | 7 | Aggregates & GROUP BY |
| **Expert** | 3 | Advanced & Real-World |
| **Total** | **25** | **Complete Coverage** |

---

## ✨ Final Tips for Interviews

1. **Ask clarifying questions** before writing queries
2. **Start simple** and build complexity
3. **Use meaningful aliases** (u for Users, o for Orders)
4. **Comment your code** - shows clear thinking
5. **Test edge cases** - NULLs, empty results, large datasets
6. **Performance matters** - Avoid nested loops, use JOINs efficiently
7. **Practice writing** these queries by hand (without running them first)

---

**Good luck with your interview! 🎯**

Practice these questions daily for 1 week and you'll master SQL SELECT! 💪
