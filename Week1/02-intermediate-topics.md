# 🎯 SQL Intermediate Topics: E-Commerce Database Edition

Complete learning path for cracking SQL interviews quickly using the E-Commerce Database.

---

## 📋 Table of Contents

1. [TOP, OFFSET-FETCH (Pagination)](#1-top-offset-fetch)
2. [String Functions](#2-string-functions)
3. [Date Functions](#3-date-functions)
4. [CASE Statement](#4-case-statement)
5. [CTE (Common Table Expression)](#5-cte)
6. [Window Functions](#6-window-functions)

---

## 1. TOP, OFFSET-FETCH

### What is TOP?

`TOP` restricts the number of rows returned from a query. Essential for pagination and finding top records.

### Basic TOP Syntax

```sql
SELECT TOP 5 *
FROM Users;
```

**Output:** First 5 users

```
UserID | UserName      | Email              | Phone      | City
-------|---------------|--------------------|------------|--------
1      | Raj Kumar     | raj@email.com      | 9876543210 | Delhi
2      | Priya Singh   | priya@email.com    | 9876543211 | Mumbai
3      | Arjun Patel   | arjun@email.com    | 9876543212 | Bangalore
4      | Neha Sharma   | neha@email.com     | 9876543213 | Hyderabad
5      | Vikram Verma  | vikram@email.com   | 9876543214 | Chennai
```

---

### TOP with ORDER BY

```sql
SELECT TOP 3 *
FROM Products
ORDER BY Price DESC;
```

**Output:** 3 most expensive products

```
ProductID | ProductName      | Category    | Price  | Stock
-----------|------------------|-------------|--------|------
6          | MacBook Pro 16"  | Electronics | 249999 | 15
2          | iPhone 15 Pro    | Electronics | 129999 | 30
5          | Dell XPS 13      | Electronics | 99999  | 25
```

---

### TOP with ORDER BY (Real Interview Question)

**Question:** Find the top 3 highest-paid products by price.

```sql
SELECT TOP 3
    ProductID,
    ProductName,
    Category,
    Price
FROM Products
ORDER BY Price DESC;
```

**Output:**
```
ProductID | ProductName      | Category    | Price
-----------|------------------|-------------|--------
6          | MacBook Pro 16"  | Electronics | 249999
2          | iPhone 15 Pro    | Electronics | 129999
5          | Dell XPS 13      | Electronics | 99999
```

---

### TOP with PERCENT

```sql
SELECT TOP 10 PERCENT *
FROM Orders
ORDER BY TotalAmount DESC;
```

**Output:** Top 10% of orders by amount (2 out of 20 orders)

```
OrderID | UserID | OrderDate  | TotalAmount | Status
--------|--------|------------|-------------|----------
12      | 8      | 2025-05-12 | 249999      | Delivered
7       | 2      | 2025-05-07 | 99999       | Delivered
```

---

### OFFSET-FETCH (SQL Server Pagination)

Used to implement pagination in web applications.

**Syntax:**
```sql
SELECT *
FROM Table
ORDER BY Column
OFFSET num ROWS
FETCH NEXT num ROWS ONLY;
```

---

### OFFSET-FETCH Example 1: Page 1

Get first 10 orders (Page 1):

```sql
SELECT 
    OrderID,
    UserID,
    OrderDate,
    TotalAmount
FROM Orders
ORDER BY OrderID
OFFSET 0 ROWS
FETCH NEXT 10 ROWS ONLY;
```

**Output:** OrderID 1-10

```
OrderID | UserID | OrderDate  | TotalAmount
--------|--------|------------|----------
1       | 1      | 2025-05-01 | 82998
2       | 2      | 2025-05-02 | 131998
3       | 3      | 2025-05-03 | 29999
...
10      | 7      | 2025-05-10 | 11999
```

---

### OFFSET-FETCH Example 2: Page 2

Get next 10 orders (Page 2):

```sql
SELECT 
    OrderID,
    UserID,
    OrderDate,
    TotalAmount
FROM Orders
ORDER BY OrderID
OFFSET 10 ROWS
FETCH NEXT 10 ROWS ONLY;
```

**Output:** OrderID 11-20

```
OrderID | UserID | OrderDate  | TotalAmount
--------|--------|------------|----------
11      | 4      | 2025-05-11 | 42998
12      | 8      | 2025-05-12 | 249999
13      | 5      | 2025-05-13 | 89998
...
20      | 8      | 2025-05-20 | 15999
```

---

### OFFSET-FETCH Interview Question

**Question:** Implement pagination to show 5 products per page. Get Page 2.

```sql
SELECT 
    ProductID,
    ProductName,
    Price,
    Stock
FROM Products
ORDER BY ProductID
OFFSET 5 ROWS
FETCH NEXT 5 ROWS ONLY;
```

**Output:** Products 6-10 (Page 2)

```
ProductID | ProductName          | Price | Stock
-----------|----------------------|-------|-------
6          | MacBook Pro 16"      | 249999| 15
7          | Nike Air Force 1     | 8999  | 150
8          | Adidas Ultraboost 22 | 11999 | 120
9          | Ray-Ban Wayfarer     | 12999 | 80
10         | Tommy Hilfiger T-Sh  | 3999  | 200
```

---

### TOP vs OFFSET-FETCH

| Feature | TOP | OFFSET-FETCH |
|---------|-----|--------------|
| **Basic Limit** | ✅ | ✅ |
| **Pagination** | ❌ | ✅ |
| **Skip Rows** | ❌ | ✅ |
| **SQL Server** | ✅ | ✅ |
| **MySQL** | ❌ (use LIMIT) | ❌ (use LIMIT) |

---

### ⚠️ SQL Server vs MySQL vs PostgreSQL

| Database | Syntax |
|----------|--------|
| **SQL Server** | `TOP 5` or `OFFSET 0 ROWS FETCH NEXT 10 ROWS ONLY` |
| **MySQL** | `LIMIT 5` |
| **PostgreSQL** | `LIMIT 5 OFFSET 10` |

---

## 2. String Functions

### What are String Functions?

Functions to manipulate text data. Crucial for extracting, cleaning, and formatting data.

### LEN() - Get String Length

Get length of user names:

```sql
SELECT 
    UserID,
    UserName,
    LEN(UserName) AS NameLength
FROM Users;
```

**Output:**
```
UserID | UserName      | NameLength
-------|---------------|----------
1      | Raj Kumar     | 9
2      | Priya Singh   | 11
3      | Arjun Patel   | 11
4      | Neha Sharma   | 11
5      | Vikram Verma  | 12
```

---

### LEFT() - Extract Left Part

Get first 5 characters of product names:

```sql
SELECT 
    ProductID,
    ProductName,
    LEFT(ProductName, 5) AS FirstFive
FROM Products
WHERE ProductID <= 5;
```

**Output:**
```
ProductID | ProductName      | FirstFive
-----------|------------------|----------
1          | Samsung Galaxy S23| Samsu
2          | iPhone 15 Pro    | iPhon
3          | Sony WH-1000XM5  | Sony
4          | Boat Airdopes 131| Boat
5          | Dell XPS 13      | Dell
```

---

### RIGHT() - Extract Right Part

Get last 3 characters of product names:

```sql
SELECT 
    ProductID,
    ProductName,
    RIGHT(ProductName, 3) AS LastThree
FROM Products
WHERE ProductID <= 5;
```

**Output:**
```
ProductID | ProductName      | LastThree
-----------|------------------|----------
1          | Samsung Galaxy S23| S23
2          | iPhone 15 Pro    | Pro
3          | Sony WH-1000XM5  | XM5
4          | Boat Airdopes 131| 131
5          | Dell XPS 13      | 13
```

---

### SUBSTRING() - Extract Middle Part

Get characters from position 2 to 5:

```sql
SELECT 
    ProductName,
    SUBSTRING(ProductName, 1, 6) AS FirstSix
FROM Products
WHERE ProductID IN (1, 2, 3);
```

**Output:**
```
ProductName          | FirstSix
---------------------|----------
Samsung Galaxy S23   | Samsun
iPhone 15 Pro        | iPhone
Sony WH-1000XM5      | Sony W
```

---

### UPPER() - Convert to Uppercase

```sql
SELECT 
    UserID,
    UserName,
    UPPER(UserName) AS NameUpperCase
FROM Users
WHERE UserID <= 3;
```

**Output:**
```
UserID | UserName      | NameUpperCase
-------|---------------|--------------
1      | Raj Kumar     | RAJ KUMAR
2      | Priya Singh   | PRIYA SINGH
3      | Arjun Patel   | ARJUN PATEL
```

---

### LOWER() - Convert to Lowercase

```sql
SELECT 
    UserID,
    Email,
    LOWER(Email) AS EmailLower
FROM Users
WHERE UserID <= 3;
```

**Output:**
```
UserID | Email              | EmailLower
-------|--------------------|-----------
1      | raj@email.com      | raj@email.com
2      | priya@email.com    | priya@email.com
3      | arjun@email.com    | arjun@email.com
```

---

### REPLACE() - Replace Text

Replace 'Electronics' with 'Gadgets':

```sql
SELECT 
    ProductID,
    ProductName,
    Category,
    REPLACE(Category, 'Electronics', 'Gadgets') AS NewCategory
FROM Products
WHERE Category = 'Electronics'
LIMIT 3;
```

**Output:**
```
ProductID | ProductName      | Category    | NewCategory
-----------|------------------|-------------|--------
1          | Samsung Galaxy S23| Electronics | Gadgets
2          | iPhone 15 Pro    | Electronics | Gadgets
3          | Sony WH-1000XM5  | Electronics | Gadgets
```

---

### LTRIM() & RTRIM() - Remove Spaces

Remove leading and trailing spaces:

```sql
SELECT 
    '  Hello World  ' AS Original,
    LTRIM('  Hello World  ') AS LeftTrimmed,
    RTRIM('  Hello World  ') AS RightTrimmed,
    LTRIM(RTRIM('  Hello World  ')) AS BothTrimmed;
```

**Output:**
```
Original           | LeftTrimmed      | RightTrimmed      | BothTrimmed
-------------------|------------------|-------------------|----------
  Hello World      | Hello World      |   Hello World     | Hello World
```

---

### CONCAT() - Combine Strings

Create full email address:

```sql
SELECT 
    UserID,
    UserName,
    City,
    CONCAT(UserName, ' from ', City) AS Description
FROM Users
WHERE UserID <= 3;
```

**Output:**
```
UserID | UserName      | City      | Description
-------|---------------|-----------|------------------
1      | Raj Kumar     | Delhi     | Raj Kumar from Delhi
2      | Priya Singh   | Mumbai    | Priya Singh from Mumbai
3      | Arjun Patel   | Bangalore | Arjun Patel from Bangalore
```

---

### 🎯 Interview Question 1: Extract Domain from Email

**Question:** Extract domain name from email addresses.

```sql
SELECT 
    UserID,
    Email,
    SUBSTRING(Email, CHARINDEX('@', Email) + 1, LEN(Email)) AS Domain
FROM Users;
```

**Output:**
```
UserID | Email              | Domain
-------|--------------------|---------
1      | raj@email.com      | email.com
2      | priya@email.com    | email.com
3      | arjun@email.com    | email.com
```

---

### 🎯 Interview Question 2: Extract First Name

**Question:** Extract first name from 'FirstName LastName' format.

```sql
SELECT 
    UserID,
    UserName,
    LEFT(UserName, CHARINDEX(' ', UserName) - 1) AS FirstName,
    SUBSTRING(UserName, CHARINDEX(' ', UserName) + 1, LEN(UserName)) AS LastName
FROM Users
WHERE UserID <= 5;
```

**Output:**
```
UserID | UserName      | FirstName | LastName
-------|---------------|-----------|--------
1      | Raj Kumar     | Raj       | Kumar
2      | Priya Singh   | Priya     | Singh
3      | Arjun Patel   | Arjun     | Patel
4      | Neha Sharma   | Neha      | Sharma
5      | Vikram Verma  | Vikram    | Verma
```

---

### 🎯 Interview Question 3: Convert Product Names to Title Case

**Question:** Convert all product names to start with capital letter.

```sql
SELECT 
    ProductID,
    ProductName,
    UPPER(LEFT(ProductName, 1)) + LOWER(SUBSTRING(ProductName, 2, LEN(ProductName))) AS TitleCase
FROM Products
WHERE ProductID <= 5;
```

**Output:**
```
ProductID | ProductName      | TitleCase
-----------|------------------|------------------
1          | Samsung Galaxy S23| Samsung galaxy s23
2          | iPhone 15 Pro    | Iphone 15 pro
3          | Sony WH-1000XM5  | Sony wh-1000xm5
4          | Boat Airdopes 131| Boat airdopes 131
5          | Dell XPS 13      | Dell xps 13
```

---

## 3. Date Functions

### What are Date Functions?

Functions to work with dates. Critical for filtering recent records, calculating age, and business analysis.

### GETDATE() - Current Date and Time

Get current date and time:

```sql
SELECT GETDATE() AS CurrentDateTime;
```

**Output:**
```
CurrentDateTime
-----------------------
2025-05-29 14:30:45.123
```

---

### DATEADD() - Add Days/Months/Years

Add 10 days to order dates:

```sql
SELECT 
    OrderID,
    OrderDate,
    DATEADD(DAY, 10, OrderDate) AS DeliveryDate
FROM Orders
WHERE OrderID <= 5;
```

**Output:**
```
OrderID | OrderDate  | DeliveryDate
--------|------------|---------------
1       | 2025-05-01 | 2025-05-11
2       | 2025-05-02 | 2025-05-12
3       | 2025-05-03 | 2025-05-13
4       | 2025-05-04 | 2025-05-14
5       | 2025-05-05 | 2025-05-15
```

---

### Add Months

Add 1 month to order dates:

```sql
SELECT 
    OrderID,
    OrderDate,
    DATEADD(MONTH, 1, OrderDate) AS NextMonth
FROM Orders
WHERE OrderID <= 3;
```

**Output:**
```
OrderID | OrderDate  | NextMonth
--------|------------|----------
1       | 2025-05-01 | 2025-06-01
2       | 2025-05-02 | 2025-06-02
3       | 2025-05-03 | 2025-06-03
```

---

### DATEDIFF() - Difference Between Dates

Calculate days since order was placed:

```sql
SELECT 
    OrderID,
    OrderDate,
    DATEDIFF(DAY, OrderDate, GETDATE()) AS DaysSinceOrder
FROM Orders;
```

**Output:**
```
OrderID | OrderDate  | DaysSinceOrder
--------|------------|---------------
1       | 2025-05-01 | 28
2       | 2025-05-02 | 27
3       | 2025-05-03 | 26
...
20      | 2025-05-20 | 9
```

---

### DATEDIFF() - Years Difference

Calculate years between dates:

```sql
SELECT 
    DATEDIFF(YEAR, '1990-01-15', GETDATE()) AS AgeInYears;
```

**Output:**
```
AgeInYears
----------
35
```

---

### YEAR(), MONTH(), DAY() - Extract Date Parts

Extract year, month, day from order dates:

```sql
SELECT 
    OrderID,
    OrderDate,
    YEAR(OrderDate) AS OrderYear,
    MONTH(OrderDate) AS OrderMonth,
    DAY(OrderDate) AS OrderDay
FROM Orders
WHERE OrderID <= 5;
```

**Output:**
```
OrderID | OrderDate  | OrderYear | OrderMonth | OrderDay
--------|------------|-----------|------------|--------
1       | 2025-05-01 | 2025      | 5          | 1
2       | 2025-05-02 | 2025      | 5          | 2
3       | 2025-05-03 | 2025      | 5          | 3
4       | 2025-05-04 | 2025      | 5          | 4
5       | 2025-05-05 | 2025      | 5          | 5
```

---

### CONVERT() - Format Dates

Convert date to different formats:

```sql
SELECT 
    OrderID,
    OrderDate,
    CONVERT(VARCHAR(10), OrderDate, 103) AS DateDDMMYYYY,
    CONVERT(VARCHAR(10), OrderDate, 120) AS DateYYYYMMDD
FROM Orders
WHERE OrderID <= 3;
```

**Output:**
```
OrderID | OrderDate  | DateDDMMYYYY | DateYYYYMMDD
--------|------------|--------------|----------
1       | 2025-05-01 | 01/05/2025   | 2025-05-01
2       | 2025-05-02 | 02/05/2025   | 2025-05-02
3       | 2025-05-03 | 03/05/2025   | 2025-05-03
```

---

### 🎯 Interview Question 1: Orders in Last 30 Days

**Question:** Find all orders placed in the last 30 days.

```sql
SELECT 
    OrderID,
    UserID,
    OrderDate,
    TotalAmount,
    DATEDIFF(DAY, OrderDate, GETDATE()) AS DaysAgo
FROM Orders
WHERE DATEDIFF(DAY, OrderDate, GETDATE()) <= 30
ORDER BY OrderDate DESC;
```

**Output:**
```
OrderID | UserID | OrderDate  | TotalAmount | DaysAgo
--------|--------|------------|-------------|--------
20      | 8      | 2025-05-20 | 15999       | 9
19      | 6      | 2025-05-19 | 22998       | 10
18      | 3      | 2025-05-18 | 44999       | 11
... (all orders within 30 days)
```

---

### 🎯 Interview Question 2: Orders This Month

**Question:** Get all orders from May 2025.

```sql
SELECT 
    OrderID,
    UserID,
    OrderDate,
    TotalAmount
FROM Orders
WHERE YEAR(OrderDate) = 2025 AND MONTH(OrderDate) = 5
ORDER BY OrderDate;
```

**Output:**
```
OrderID | UserID | OrderDate  | TotalAmount
--------|--------|------------|----------
1       | 1      | 2025-05-01 | 82998
2       | 2      | 2025-05-02 | 131998
3       | 3      | 2025-05-03 | 29999
... (all orders in May 2025)
```

---

### 🎯 Interview Question 3: Calculate Expected Delivery Date

**Question:** Assuming 7-day delivery, show expected delivery date for all orders.

```sql
SELECT 
    OrderID,
    UserID,
    OrderDate,
    DATEADD(DAY, 7, OrderDate) AS ExpectedDeliveryDate,
    Status
FROM Orders
WHERE Status IN ('Pending', 'Shipped')
ORDER BY OrderDate;
```

**Output:**
```
OrderID | UserID | OrderDate  | ExpectedDeliveryDate | Status
--------|--------|------------|----------------------|--------
4       | 4      | 2025-05-04 | 2025-05-11           | Pending
8       | 3      | 2025-05-08 | 2025-05-15           | Pending
13      | 5      | 2025-05-13 | 2025-05-20           | Pending
15      | 9      | 2025-05-15 | 2025-05-22           | Shipped
20      | 8      | 2025-05-20 | 2025-05-27           | Shipped
```

---

## 4. CASE Statement

### What is CASE?

Conditional logic to assign values based on conditions. Like `IF-ELSE` in programming.

### Basic CASE Syntax

```sql
SELECT 
    ColumnName,
    CASE
        WHEN Condition1 THEN Value1
        WHEN Condition2 THEN Value2
        ELSE Value3
    END AS NewColumnName
FROM Table;
```

---

### CASE Example 1: Categorize Orders by Amount

```sql
SELECT 
    OrderID,
    UserID,
    TotalAmount,
    CASE
        WHEN TotalAmount > 100000 THEN 'Premium'
        WHEN TotalAmount > 50000 THEN 'High'
        WHEN TotalAmount > 20000 THEN 'Medium'
        ELSE 'Low'
    END AS OrderCategory
FROM Orders
ORDER BY TotalAmount DESC;
```

**Output:**
```
OrderID | UserID | TotalAmount | OrderCategory
--------|--------|-------------|---------------
12      | 8      | 249999      | Premium
2       | 2      | 131998      | Premium
16      | 10     | 129999      | Premium
7       | 2      | 99999       | High
13      | 5      | 89998       | High
1       | 1      | 82998       | High
9       | 6      | 64999       | High
17      | 2      | 64999       | High
18      | 3      | 44999       | High
11      | 4      | 42998       | High
15      | 9      | 34998       | Medium
3       | 3      | 29999       | Medium
8       | 3      | 49999       | High
6       | 1      | 20998       | Medium
19      | 6      | 22998       | Medium
5       | 5      | 12998       | Low
10      | 7      | 11999       | Low
20      | 8      | 15999       | Low
14      | 1      | 12999       | Low
4       | 4      | 54998       | High
```

---

### CASE Example 2: Order Status Description

```sql
SELECT 
    OrderID,
    OrderDate,
    Status,
    CASE
        WHEN Status = 'Delivered' THEN 'Order has arrived'
        WHEN Status = 'Shipped' THEN 'Order is on the way'
        WHEN Status = 'Pending' THEN 'Order is being prepared'
        ELSE 'Unknown status'
    END AS StatusDescription
FROM Orders
ORDER BY OrderID;
```

**Output:**
```
OrderID | OrderDate  | Status    | StatusDescription
--------|------------|-----------|----------------------
1       | 2025-05-01 | Delivered | Order has arrived
2       | 2025-05-02 | Delivered | Order has arrived
3       | 2025-05-03 | Delivered | Order has arrived
4       | 2025-05-04 | Pending   | Order is being prepared
5       | 2025-05-05 | Delivered | Order has arrived
6       | 2025-05-06 | Shipped   | Order is on the way
...
```

---

### CASE Example 3: Categorize Products by Price

```sql
SELECT 
    ProductID,
    ProductName,
    Price,
    CASE
        WHEN Price >= 200000 THEN 'Premium Electronics'
        WHEN Price >= 100000 THEN 'High-End'
        WHEN Price >= 50000 THEN 'Mid-Range'
        WHEN Price >= 20000 THEN 'Budget'
        ELSE 'Affordable'
    END AS PriceCategory
FROM Products
ORDER BY Price DESC;
```

**Output:**
```
ProductID | ProductName          | Price  | PriceCategory
-----------|----------------------|--------|------------------
6          | MacBook Pro 16"      | 249999 | Premium Electronics
2          | iPhone 15 Pro        | 129999 | High-End
5          | Dell XPS 13          | 99999  | High-End
1          | Samsung Galaxy S23   | 79999  | Mid-Range
14         | Canon EOS M6         | 64999  | Mid-Range
9          | Ray-Ban Wayfarer     | 12999  | Budget
16         | Kindle Paperwhite    | 13999  | Budget
13         | Harman Kardon Speaker| 49999  | Mid-Range
...
```

---

### CASE Example 4: Discount Based on Category

```sql
SELECT 
    ProductID,
    ProductName,
    Category,
    Price,
    CASE
        WHEN Category = 'Electronics' THEN ROUND(Price * 0.10, 2)
        WHEN Category = 'Fashion' THEN ROUND(Price * 0.20, 2)
        ELSE 0
    END AS Discount,
    CASE
        WHEN Category = 'Electronics' THEN ROUND(Price * 0.90, 2)
        WHEN Category = 'Fashion' THEN ROUND(Price * 0.80, 2)
        ELSE Price
    END AS FinalPrice
FROM Products
WHERE ProductID <= 10;
```

**Output:**
```
ProductID | ProductName          | Category    | Price | Discount | FinalPrice
-----------|----------------------|-------------|-------|----------|----------
1          | Samsung Galaxy S23   | Electronics | 79999 | 8000     | 71999
2          | iPhone 15 Pro        | Electronics | 129999| 13000    | 116999
3          | Sony WH-1000XM5      | Electronics | 29999 | 3000     | 26999
4          | Boat Airdopes 131    | Electronics | 2999  | 300      | 2699
5          | Dell XPS 13          | Electronics | 99999 | 10000    | 89999
6          | MacBook Pro 16"      | Electronics | 249999| 25000    | 224999
7          | Nike Air Force 1     | Fashion     | 8999  | 1800     | 7199
8          | Adidas Ultraboost 22 | Fashion     | 11999 | 2400     | 9599
9          | Ray-Ban Wayfarer     | Fashion     | 12999 | 2600     | 10399
10         | Tommy Hilfiger T-Sh  | Fashion     | 3999  | 800      | 3199
```

---

### 🎯 Interview Question 1: Profit Margin Category

**Question:** Categorize products as 'High Margin' (price > 50000), 'Medium Margin' (price 20000-50000), or 'Low Margin'.

```sql
SELECT 
    ProductID,
    ProductName,
    Price,
    CASE
        WHEN Price > 50000 THEN 'High Margin'
        WHEN Price >= 20000 THEN 'Medium Margin'
        ELSE 'Low Margin'
    END AS MarginCategory
FROM Products
ORDER BY Price DESC;
```

**Output:** (First 10 rows)
```
ProductID | ProductName          | Price  | MarginCategory
-----------|----------------------|--------|------------------
6          | MacBook Pro 16"      | 249999 | High Margin
2          | iPhone 15 Pro        | 129999 | High Margin
5          | Dell XPS 13          | 99999  | High Margin
1          | Samsung Galaxy S23   | 79999  | High Margin
14         | Canon EOS M6         | 64999  | High Margin
13         | Harman Kardon Speaker| 49999  | Medium Margin
15         | GoPro Hero 12        | 44999  | Medium Margin
17         | Apple Watch Series 9 | 41999  | Medium Margin
3          | Sony WH-1000XM5      | 29999  | Medium Margin
12         | Zara Winter Jacket   | 15999  | Medium Margin
```

---

### 🎯 Interview Question 2: Customer Loyalty Status

**Question:** Assign loyalty status based on total spending.

```sql
SELECT 
    u.UserID,
    u.UserName,
    COUNT(o.OrderID) AS TotalOrders,
    SUM(o.TotalAmount) AS TotalSpent,
    CASE
        WHEN SUM(o.TotalAmount) >= 200000 THEN 'Gold'
        WHEN SUM(o.TotalAmount) >= 100000 THEN 'Silver'
        WHEN SUM(o.TotalAmount) >= 50000 THEN 'Bronze'
        ELSE 'Regular'
    END AS LoyaltyStatus
FROM Users u
LEFT JOIN Orders o ON u.UserID = o.UserID
GROUP BY u.UserID, u.UserName
ORDER BY TotalSpent DESC;
```

**Output:**
```
UserID | UserName      | TotalOrders | TotalSpent | LoyaltyStatus
-------|---------------|-------------|------------|---------------
1      | Raj Kumar     | 3           | 116995     | Silver
8      | Divya Nair    | 2           | 265998     | Gold
2      | Priya Singh   | 3           | 296996     | Gold
3      | Arjun Patel   | 3           | 119997     | Silver
4      | Neha Sharma   | 2           | 97996      | Bronze
5      | Vikram Verma  | 2           | 102996     | Silver
6      | Anjali Reddy  | 2           | 87997      | Bronze
7      | Rohit Kumar   | 1           | 11999      | Regular
9      | Sanjay Singh  | 1           | 34998      | Regular
10     | Pooja Gupta   | 1           | 129999     | Silver
```

---

## 5. CTE (Common Table Expression)

### What is CTE?

A temporary result set that can be referenced in a SELECT, INSERT, UPDATE, or DELETE query. Like defining a temporary view.

### Basic CTE Syntax

```sql
WITH CTEName AS (
    SELECT column1, column2, ...
    FROM table
    WHERE condition
)
SELECT *
FROM CTEName;
```

---

### CTE Example 1: High-Value Orders

```sql
WITH HighValueOrders AS (
    SELECT 
        OrderID,
        UserID,
        OrderDate,
        TotalAmount
    FROM Orders
    WHERE TotalAmount > 50000
)
SELECT 
    hvo.OrderID,
    hvo.UserID,
    u.UserName,
    hvo.OrderDate,
    hvo.TotalAmount
FROM HighValueOrders hvo
INNER JOIN Users u ON hvo.UserID = u.UserID
ORDER BY hvo.TotalAmount DESC;
```

**Output:**
```
OrderID | UserID | UserName      | OrderDate  | TotalAmount
--------|--------|---------------|------------|----------
12      | 8      | Divya Nair    | 2025-05-12 | 249999
2       | 2      | Priya Singh   | 2025-05-02 | 131998
16      | 10     | Pooja Gupta   | 2025-05-16 | 129999
7       | 2      | Priya Singh   | 2025-05-07 | 99999
13      | 5      | Vikram Verma  | 2025-05-13 | 89998
1       | 1      | Raj Kumar     | 2025-05-01 | 82998
9       | 6      | Anjali Reddy  | 2025-05-09 | 64999
17      | 2      | Priya Singh   | 2025-05-17 | 64999
18      | 3      | Arjun Patel   | 2025-05-18 | 44999
11      | 4      | Neha Sharma   | 2025-05-11 | 42998
```

---

### CTE Example 2: Premium Products (Price > 100000)

```sql
WITH PremiumProducts AS (
    SELECT 
        ProductID,
        ProductName,
        Category,
        Price,
        Stock
    FROM Products
    WHERE Price > 100000
)
SELECT 
    pp.ProductID,
    pp.ProductName,
    pp.Category,
    pp.Price,
    pp.Stock
FROM PremiumProducts pp
ORDER BY pp.Price DESC;
```

**Output:**
```
ProductID | ProductName      | Category    | Price  | Stock
-----------|------------------|-------------|--------|------
6          | MacBook Pro 16"  | Electronics | 249999 | 15
2          | iPhone 15 Pro    | Electronics | 129999 | 30
5          | Dell XPS 13      | Electronics | 99999  | 25
```

---

### CTE Example 3: Active Users (Who Placed Orders)

```sql
WITH ActiveUsers AS (
    SELECT DISTINCT
        u.UserID,
        u.UserName,
        u.Email,
        u.City
    FROM Users u
    INNER JOIN Orders o ON u.UserID = o.UserID
)
SELECT 
    au.UserID,
    au.UserName,
    au.City,
    COUNT(o.OrderID) AS TotalOrders,
    SUM(o.TotalAmount) AS TotalSpent
FROM ActiveUsers au
LEFT JOIN Orders o ON au.UserID = o.UserID
GROUP BY au.UserID, au.UserName, au.City
ORDER BY TotalSpent DESC;
```

**Output:**
```
UserID | UserName      | City      | TotalOrders | TotalSpent
-------|---------------|-----------|-------------|----------
2      | Priya Singh   | Mumbai    | 3           | 296996
8      | Divya Nair    | Ahmedabad | 2           | 265998
1      | Raj Kumar     | Delhi     | 3           | 116995
3      | Arjun Patel   | Bangalore | 3           | 119997
4      | Neha Sharma   | Hyderabad | 2           | 97996
5      | Vikram Verma  | Chennai   | 2           | 102996
6      | Anjali Reddy  | Pune      | 2           | 87997
7      | Rohit Kumar   | Kolkata   | 1           | 11999
9      | Sanjay Singh  | Jaipur    | 1           | 34998
10     | Pooja Gupta   | Lucknow   | 1           | 129999
```

---

### CTE Example 4: Multiple CTEs (Products Sold + Order Count)

```sql
WITH ProductSales AS (
    SELECT 
        p.ProductID,
        p.ProductName,
        p.Price,
        COUNT(oi.OrderID) AS TimesSold,
        SUM(oi.Quantity) AS TotalQuantity
    FROM Products p
    LEFT JOIN OrderItems oi ON p.ProductID = oi.ProductID
    GROUP BY p.ProductID, p.ProductName, p.Price
),
PopularProducts AS (
    SELECT 
        ProductID,
        ProductName,
        Price,
        TimesSold,
        TotalQuantity
    FROM ProductSales
    WHERE TimesSold > 0
)
SELECT 
    pp.ProductID,
    pp.ProductName,
    pp.Price,
    pp.TimesSold,
    pp.TotalQuantity
FROM PopularProducts pp
ORDER BY pp.TimesSold DESC;
```

**Output:**
```
ProductID | ProductName          | Price | TimesSold | TotalQuantity
-----------|----------------------|-------|-----------|---------------
4          | Boat Airdopes 131    | 2999  | 3         | 3
2          | iPhone 15 Pro        | 129999| 2         | 2
6          | MacBook Pro 16"      | 249999| 2         | 2
3          | Sony WH-1000XM5      | 29999 | 2         | 2
...
```

---

### 🎯 Interview Question 1: Find Customers Who Spent > Average

**Question:** Find customers whose total spending is above average.

```sql
WITH CustomerSpending AS (
    SELECT 
        u.UserID,
        u.UserName,
        u.City,
        SUM(o.TotalAmount) AS TotalSpent
    FROM Users u
    LEFT JOIN Orders o ON u.UserID = o.UserID
    GROUP BY u.UserID, u.UserName, u.City
),
AverageSpending AS (
    SELECT AVG(TotalSpent) AS AvgSpend
    FROM CustomerSpending
    WHERE TotalSpent IS NOT NULL
)
SELECT 
    cs.UserID,
    cs.UserName,
    cs.City,
    cs.TotalSpent,
    ROUND(asng.AvgSpend, 2) AS AvgSpending,
    ROUND(cs.TotalSpent - asng.AvgSpend, 2) AS AboveAverage
FROM CustomerSpending cs
CROSS JOIN AverageSpending asng
WHERE cs.TotalSpent > asng.AvgSpend
ORDER BY cs.TotalSpent DESC;
```

**Output:**
```
UserID | UserName      | City      | TotalSpent | AvgSpending | AboveAverage
-------|---------------|-----------|------------|-------------|----------
2      | Priya Singh   | Mumbai    | 296996     | 111095.55   | 185900.45
8      | Divya Nair    | Ahmedabad | 265998     | 111095.55   | 154902.45
1      | Raj Kumar     | Delhi     | 116995     | 111095.55   | 5899.45
3      | Arjun Patel   | Bangalore | 119997     | 111095.55   | 8901.45
```

---

### 🎯 Interview Question 2: Top 3 Products by Sales

**Question:** Find top 3 best-selling products.

```sql
WITH ProductSales AS (
    SELECT 
        p.ProductID,
        p.ProductName,
        p.Category,
        SUM(oi.Quantity) AS TotalQuantitySold
    FROM Products p
    LEFT JOIN OrderItems oi ON p.ProductID = oi.ProductID
    GROUP BY p.ProductID, p.ProductName, p.Category
)
SELECT TOP 3
    ProductID,
    ProductName,
    Category,
    TotalQuantitySold
FROM ProductSales
WHERE TotalQuantitySold > 0
ORDER BY TotalQuantitySold DESC;
```

**Output:**
```
ProductID | ProductName          | Category    | TotalQuantitySold
-----------|----------------------|-------------|------------------
4          | Boat Airdopes 131    | Electronics | 3
2          | iPhone 15 Pro        | Electronics | 2
6          | MacBook Pro 16"      | Electronics | 2
```

---

## 6. Window Functions

### What are Window Functions?

Functions that perform calculations across a set of rows (window) that are related to the current row. Powerful for ranking, running totals, and analytics.

### ROW_NUMBER() - Unique Row Numbers

Assign unique sequential numbers to rows:

```sql
SELECT 
    OrderID,
    UserID,
    TotalAmount,
    ROW_NUMBER() OVER (ORDER BY TotalAmount DESC) AS RN
FROM Orders;
```

**Output:**
```
OrderID | UserID | TotalAmount | RN
--------|--------|-------------|----
12      | 8      | 249999      | 1
2       | 2      | 131998      | 2
16      | 10     | 129999      | 3
7       | 2      | 99999       | 4
13      | 5      | 89998       | 5
1       | 1      | 82998       | 6
9       | 6      | 64999       | 7
17      | 2      | 64999       | 8
18      | 3      | 44999       | 9
11      | 4      | 42998       | 10
```

---

### ROW_NUMBER() with PARTITION BY

Rank orders per user:

```sql
SELECT 
    OrderID,
    UserID,
    OrderDate,
    TotalAmount,
    ROW_NUMBER() OVER (PARTITION BY UserID ORDER BY OrderDate) AS OrderNumber
FROM Orders
ORDER BY UserID, OrderNumber;
```

**Output:**
```
OrderID | UserID | OrderDate  | TotalAmount | OrderNumber
--------|--------|------------|-------------|----------
1       | 1      | 2025-05-01 | 82998       | 1
6       | 1      | 2025-05-06 | 20998       | 2
14      | 1      | 2025-05-14 | 12999       | 3
2       | 2      | 2025-05-02 | 131998      | 1
7       | 2      | 2025-05-07 | 99999       | 2
17      | 2      | 2025-05-17 | 64999       | 3
3       | 3      | 2025-05-03 | 29999       | 1
8       | 3      | 2025-05-08 | 49999       | 2
18      | 3      | 2025-05-18 | 44999       | 3
...
```

---

### RANK() - Rank with Ties

Handles duplicate values by giving same rank:

```sql
SELECT 
    ProductID,
    ProductName,
    Price,
    RANK() OVER (ORDER BY Price DESC) AS PriceRank
FROM Products
WHERE ProductID <= 10;
```

**Output:**
```
ProductID | ProductName          | Price  | PriceRank
-----------|----------------------|--------|----------
6          | MacBook Pro 16"      | 249999 | 1
2          | iPhone 15 Pro        | 129999 | 2
5          | Dell XPS 13          | 99999  | 3
1          | Samsung Galaxy S23   | 79999  | 4
3          | Sony WH-1000XM5      | 29999  | 5
8          | Adidas Ultraboost 22 | 11999  | 6
9          | Ray-Ban Wayfarer     | 12999  | 6
4          | Boat Airdopes 131    | 2999   | 8
10         | Tommy Hilfiger T-Sh  | 3999   | 7
```

---

### DENSE_RANK() - Consecutive Ranking

No gaps in ranking even with ties:

```sql
SELECT 
    ProductID,
    ProductName,
    Price,
    DENSE_RANK() OVER (ORDER BY Price DESC) AS DenseRank
FROM Products
WHERE ProductID <= 10;
```

**Output:**
```
ProductID | ProductName          | Price  | DenseRank
-----------|----------------------|--------|----------
6          | MacBook Pro 16"      | 249999 | 1
2          | iPhone 15 Pro        | 129999 | 2
5          | Dell XPS 13          | 99999  | 3
1          | Samsung Galaxy S23   | 79999  | 4
3          | Sony WH-1000XM5      | 29999  | 5
8          | Adidas Ultraboost 22 | 11999  | 6
9          | Ray-Ban Wayfarer     | 12999  | 6
10         | Tommy Hilfiger T-Sh  | 3999   | 7
4          | Boat Airdopes 131    | 2999   | 8
```

---

### Comparison: ROW_NUMBER() vs RANK() vs DENSE_RANK()

Products with their price ranking:

```sql
SELECT 
    ProductID,
    ProductName,
    Price,
    ROW_NUMBER() OVER (ORDER BY Price DESC) AS RN,
    RANK() OVER (ORDER BY Price DESC) AS RK,
    DENSE_RANK() OVER (ORDER BY Price DESC) AS DR
FROM (
    SELECT DISTINCT ProductID, ProductName, Price FROM Products
) AS DistinctPrices
WHERE ProductID IN (6, 2, 5, 1, 3, 8, 9, 4, 10)
ORDER BY Price DESC;
```

**Comparison Table:**

| ProductName | Price | ROW_NUMBER | RANK | DENSE_RANK |
|---|---|---|---|---|
| MacBook Pro 16" | 249999 | 1 | 1 | 1 |
| iPhone 15 Pro | 129999 | 2 | 2 | 2 |
| Dell XPS 13 | 99999 | 3 | 3 | 3 |
| Samsung Galaxy S23 | 79999 | 4 | 4 | 4 |
| Sony WH-1000XM5 | 29999 | 5 | 5 | 5 |
| Adidas Ultraboost 22 | 11999 | 6 | 6 | 6 |
| Ray-Ban Wayfarer | 12999 | 7 | 6 | 6 |
| Tommy Hilfiger T-Sh | 3999 | 8 | 8 | 7 |
| Boat Airdopes 131 | 2999 | 9 | 9 | 8 |

---

### LAG() - Previous Row Value

Get previous order amount:

```sql
SELECT 
    OrderID,
    UserID,
    TotalAmount,
    LAG(TotalAmount) OVER (PARTITION BY UserID ORDER BY OrderDate) AS PreviousOrderAmount,
    TotalAmount - LAG(TotalAmount) OVER (PARTITION BY UserID ORDER BY OrderDate) AS DifferencefromPrevious
FROM Orders
WHERE UserID <= 3
ORDER BY UserID, OrderID;
```

**Output:**
```
OrderID | UserID | TotalAmount | PreviousOrderAmount | DifferencefromPrevious
--------|--------|-------------|---------------------|--------------------
1       | 1      | 82998       | NULL                | NULL
6       | 1      | 20998       | 82998               | -62000
14      | 1      | 12999       | 20998               | -8000
2       | 2      | 131998      | NULL                | NULL
7       | 2      | 99999       | 131998              | -32000
17      | 2      | 64999       | 99999               | -35000
3       | 3      | 29999       | NULL                | NULL
8       | 3      | 49999       | 29999               | 20000
18      | 3      | 44999       | 49999               | -5000
```

---

### LEAD() - Next Row Value

Get next order date:

```sql
SELECT 
    OrderID,
    UserID,
    OrderDate,
    LEAD(OrderDate) OVER (PARTITION BY UserID ORDER BY OrderDate) AS NextOrderDate,
    DATEDIFF(DAY, OrderDate, LEAD(OrderDate) OVER (PARTITION BY UserID ORDER BY OrderDate)) AS DaysBetweenOrders
FROM Orders
WHERE UserID <= 3
ORDER BY UserID, OrderID;
```

**Output:**
```
OrderID | UserID | OrderDate  | NextOrderDate | DaysBetweenOrders
--------|--------|------------|---------------|------------------
1       | 1      | 2025-05-01 | 2025-05-06    | 5
6       | 1      | 2025-05-06 | 2025-05-14    | 8
14      | 1      | 2025-05-14 | NULL          | NULL
2       | 2      | 2025-05-02 | 2025-05-07    | 5
7       | 2      | 2025-05-07 | 2025-05-17    | 10
17      | 2      | 2025-05-17 | NULL          | NULL
3       | 3      | 2025-05-03 | 2025-05-08    | 5
8       | 3      | 2025-05-08 | 2025-05-18    | 10
18      | 3      | 2025-05-18 | NULL          | NULL
```

---

### SUM() OVER - Running Total

Calculate cumulative order amount per user:

```sql
SELECT 
    OrderID,
    UserID,
    OrderDate,
    TotalAmount,
    SUM(TotalAmount) OVER (PARTITION BY UserID ORDER BY OrderDate) AS RunningTotal
FROM Orders
WHERE UserID IN (1, 2)
ORDER BY UserID, OrderDate;
```

**Output:**
```
OrderID | UserID | OrderDate  | TotalAmount | RunningTotal
--------|--------|------------|-------------|----------
1       | 1      | 2025-05-01 | 82998       | 82998
6       | 1      | 2025-05-06 | 20998       | 103996
14      | 1      | 2025-05-14 | 12999       | 116995
2       | 2      | 2025-05-02 | 131998      | 131998
7       | 2      | 2025-05-07 | 99999       | 231997
17      | 2      | 2025-05-17 | 64999       | 296996
```

---

### AVG() OVER - Running Average

Calculate rolling average:

```sql
SELECT 
    OrderID,
    UserID,
    OrderDate,
    TotalAmount,
    ROUND(AVG(TotalAmount) OVER (PARTITION BY UserID ORDER BY OrderDate), 2) AS RunningAverage
FROM Orders
WHERE UserID IN (1, 2)
ORDER BY UserID, OrderDate;
```

**Output:**
```
OrderID | UserID | OrderDate  | TotalAmount | RunningAverage
--------|--------|------------|-------------|----------
1       | 1      | 2025-05-01 | 82998       | 82998.00
6       | 1      | 2025-05-06 | 20998       | 51998.00
14      | 1      | 2025-05-14 | 12999       | 38998.33
2       | 2      | 2025-05-02 | 131998      | 131998.00
7       | 2      | 2025-05-07 | 99999       | 115998.50
17      | 2      | 2025-05-17 | 64999       | 98998.67
```

---

### 🎯 Interview Question 1: Second Highest Salary Problem

**Question:** Find the product with second-highest price.

```sql
WITH ProductRanked AS (
    SELECT 
        ProductID,
        ProductName,
        Price,
        DENSE_RANK() OVER (ORDER BY Price DESC) AS PriceRank
    FROM Products
)
SELECT 
    ProductID,
    ProductName,
    Price
FROM ProductRanked
WHERE PriceRank = 2;
```

**Output:**
```
ProductID | ProductName      | Price
-----------|------------------|--------
2          | iPhone 15 Pro    | 129999
```

---

### 🎯 Interview Question 2: Top N Records Per Category

**Question:** Find top 2 most expensive products in each category.

```sql
WITH ProductRanked AS (
    SELECT 
        ProductID,
        ProductName,
        Category,
        Price,
        ROW_NUMBER() OVER (PARTITION BY Category ORDER BY Price DESC) AS RN
    FROM Products
)
SELECT 
    ProductID,
    ProductName,
    Category,
    Price
FROM ProductRanked
WHERE RN <= 2
ORDER BY Category, Price DESC;
```

**Output:**
```
ProductID | ProductName           | Category    | Price
-----------|----------------------|-------------|--------
6          | MacBook Pro 16"       | Electronics | 249999
2          | iPhone 15 Pro         | Electronics | 129999
12         | Zara Winter Jacket    | Fashion     | 15999
9          | Ray-Ban Wayfarer      | Fashion     | 12999
```

---

### 🎯 Interview Question 3: Duplicate Records Detection

**Question:** Find products that appear multiple times in the same price range.

```sql
WITH ProductFrequency AS (
    SELECT 
        ProductName,
        Price,
        COUNT(*) AS Frequency,
        ROW_NUMBER() OVER (ORDER BY ProductName) AS RN
    FROM Products
    GROUP BY ProductName, Price
    HAVING COUNT(*) > 1
)
SELECT 
    ProductName,
    Price,
    Frequency
FROM ProductFrequency;
```

**Note:** In our data, there are no duplicates, so this returns 0 rows. But the concept is important for interviews.

---

### 🎯 Interview Question 4: Customers Who Bought Specific Product

**Question:** Find customers who bought 'iPhone 15 Pro' and rank them by purchase date.

```sql
WITH iPhoneBuyers AS (
    SELECT 
        u.UserID,
        u.UserName,
        u.City,
        p.ProductName,
        o.OrderDate,
        ROW_NUMBER() OVER (PARTITION BY u.UserID ORDER BY o.OrderDate DESC) AS PurchaseOrder
    FROM Users u
    INNER JOIN Orders o ON u.UserID = o.UserID
    INNER JOIN OrderItems oi ON o.OrderID = oi.OrderID
    INNER JOIN Products p ON oi.ProductID = p.ProductID
    WHERE p.ProductName = 'iPhone 15 Pro'
)
SELECT 
    UserID,
    UserName,
    City,
    ProductName,
    OrderDate,
    PurchaseOrder
FROM iPhoneBuyers
ORDER BY OrderDate DESC;
```

**Output:**
```
UserID | UserName      | City      | ProductName      | OrderDate  | PurchaseOrder
-------|---------------|-----------|------------------|------------|---------------
2      | Priya Singh   | Mumbai    | iPhone 15 Pro    | 2025-05-13 | 1
10     | Pooja Gupta   | Lucknow   | iPhone 15 Pro    | 2025-05-16 | 1
2      | Priya Singh   | Mumbai    | iPhone 15 Pro    | 2025-05-02 | 2
```

---

## 🎯 10 MUST-PRACTICE Interview Problems

### Problem 1: Highest Salary (Highest Price Product)

Find the product with the highest price:

```sql
SELECT TOP 1
    ProductID,
    ProductName,
    Price
FROM Products
ORDER BY Price DESC;
```

---

### Problem 2: Second Highest Salary (Second Highest Price)

```sql
WITH ProductRanked AS (
    SELECT 
        ProductID,
        ProductName,
        Price,
        DENSE_RANK() OVER (ORDER BY Price DESC) AS PriceRank
    FROM Products
)
SELECT 
    ProductID,
    ProductName,
    Price
FROM ProductRanked
WHERE PriceRank = 2;
```

---

### Problem 3: Nth Highest Salary (Nth Highest Price)

Find 3rd highest priced product:

```sql
WITH ProductRanked AS (
    SELECT 
        ProductID,
        ProductName,
        Price,
        DENSE_RANK() OVER (ORDER BY Price DESC) AS PriceRank
    FROM Products
)
SELECT 
    ProductID,
    ProductName,
    Price
FROM ProductRanked
WHERE PriceRank = 3;
```

---

### Problem 4: Duplicate Records

Find products with duplicate names:

```sql
SELECT 
    ProductName,
    COUNT(*) AS Count
FROM Products
GROUP BY ProductName
HAVING COUNT(*) > 1;
```

---

### Problem 5: Delete Duplicates (Keep Latest)

Delete duplicate products keeping the highest ProductID:

```sql
DELETE FROM Products
WHERE ProductID NOT IN (
    SELECT MAX(ProductID)
    FROM Products
    GROUP BY ProductName
);
```

---

### Problem 6: Top 3 Products per Category

```sql
WITH ProductRanked AS (
    SELECT 
        ProductID,
        ProductName,
        Category,
        Price,
        ROW_NUMBER() OVER (PARTITION BY Category ORDER BY Price DESC) AS RN
    FROM Products
)
SELECT 
    ProductID,
    ProductName,
    Category,
    Price
FROM ProductRanked
WHERE RN <= 3
ORDER BY Category, Price DESC;
```

---

### Problem 7: Running Total of Orders

```sql
SELECT 
    OrderID,
    UserID,
    OrderDate,
    TotalAmount,
    SUM(TotalAmount) OVER (ORDER BY OrderDate) AS RunningTotal
FROM Orders
ORDER BY OrderDate;
```

---

### Problem 8: Orders in Last 30 Days

```sql
SELECT 
    OrderID,
    UserID,
    OrderDate,
    TotalAmount,
    DATEDIFF(DAY, OrderDate, GETDATE()) AS DaysAgo
FROM Orders
WHERE DATEDIFF(DAY, OrderDate, GETDATE()) <= 30
ORDER BY OrderDate DESC;
```

---

### Problem 9: Orders Above Average Order Value

```sql
WITH OrderStats AS (
    SELECT 
        OrderID,
        UserID,
        TotalAmount,
        AVG(TotalAmount) OVER () AS AvgOrder
    FROM Orders
)
SELECT 
    OrderID,
    UserID,
    TotalAmount,
    AvgOrder
FROM OrderStats
WHERE TotalAmount > AvgOrder
ORDER BY TotalAmount DESC;
```

---

### Problem 10: Customer Spending More Than Their Manager/Average

```sql
WITH CustomerSpending AS (
    SELECT 
        u.UserID,
        u.UserName,
        SUM(o.TotalAmount) AS TotalSpent
    FROM Users u
    LEFT JOIN Orders o ON u.UserID = o.UserID
    GROUP BY u.UserID, u.UserName
),
AverageSpending AS (
    SELECT AVG(TotalSpent) AS AvgSpend
    FROM CustomerSpending
    WHERE TotalSpent IS NOT NULL
)
SELECT 
    cs.UserID,
    cs.UserName,
    cs.TotalSpent
FROM CustomerSpending cs
CROSS JOIN AverageSpending a
WHERE cs.TotalSpent > a.AvgSpend
ORDER BY cs.TotalSpent DESC;
```

---

## 🏆 Summary Table

| Topic | Key Concept | Interview Frequency |
|-------|-----------|---------------------|
| **TOP** | Limit rows | ⭐⭐⭐ |
| **OFFSET-FETCH** | Pagination | ⭐⭐⭐⭐ |
| **String Functions** | Text manipulation | ⭐⭐⭐ |
| **Date Functions** | Date calculations | ⭐⭐⭐⭐ |
| **CASE** | Conditional logic | ⭐⭐⭐⭐ |
| **CTE** | Temp tables | ⭐⭐⭐⭐⭐ |
| **Window Functions** | Ranking/Analytics | ⭐⭐⭐⭐⭐ |

---

## ✅ What You Now Know

After completing this guide, you can:

✅ Use TOP and OFFSET-FETCH for pagination  
✅ Manipulate strings with 10+ functions  
✅ Calculate dates and differences  
✅ Apply conditional logic with CASE  
✅ Write reusable CTEs  
✅ Rank data with window functions  
✅ Solve 10 classic interview problems  

---

## 🚀 Next Steps

1. **Practice each topic** with our E-Commerce database
2. **Combine multiple concepts** in complex queries
3. **Practice the 10 must-solve problems** until comfortable
4. **Attempt real interview questions** from LeetCode or HackerRank
5. **Learn JOINS in depth** (covered in next section)

**You're ready for intermediate SQL interview rounds!** 🎉
