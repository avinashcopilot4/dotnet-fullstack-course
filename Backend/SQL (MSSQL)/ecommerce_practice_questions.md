# 🎯 E-Commerce Database - SQL Practice Questions

## Complete Question Bank for Learning SQL Concepts

---

## 📚 Table of Contents
1. [Beginner Level (Basic SELECT & Filtering)](#beginner)
2. [Intermediate Level (JOINs & GROUP BY)](#intermediate)
3. [Advanced Level (Subqueries & Complex Logic)](#advanced)
4. [Expert Level (Window Functions & Optimization)](#expert)
5. [Challenge Problems](#challenges)

---

## <a id="beginner"></a>🟢 BEGINNER LEVEL - Basic SELECT & Filtering

### 1. List all users with their contact information
```sql
-- Expected Output: UserID, UserName, Email, Phone, City (10 rows)
SELECT UserID, UserName, Email, Phone, City FROM Users;
```
**Concepts:** Basic SELECT, All columns

---

### 2. Find all products in the Electronics category
```sql
-- Expected Output: ProductID, ProductName, Price, Stock
-- Should return 14 products
```
**Concepts:** WHERE clause, filtering by category

---

### 3. Get all orders with "Delivered" status
```sql
-- Expected Output: OrderID, UserID, OrderDate, TotalAmount, Status
-- Should return specific delivered orders
```
**Concepts:** WHERE clause with text matching

---

### 4. List all Fashion products under ₹10,000
```sql
-- Expected Output: ProductName, Category, Price, Stock
-- Should return items like Nike Air Force 1, Tommy Hilfiger T-Shirt, etc.
```
**Concepts:** WHERE with AND operator, price filtering

---

### 5. Find all users from Delhi or Mumbai
```sql
-- Expected Output: UserName, City, Email, Phone
-- Should return 2 users
```
**Concepts:** WHERE with OR operator

---

### 6. Get the top 5 most expensive products
```sql
-- Expected Output: ProductName, Price, Category
-- Ordered from highest to lowest price
```
**Concepts:** ORDER BY DESC, TOP 5

---

### 7. Find products with stock less than 50 units
```sql
-- Expected Output: ProductName, Stock, Category, Price
```
**Concepts:** WHERE with comparison operators

---

### 8. List all unique cities where users are located
```sql
-- Expected Output: Unique city names (10 cities)
```
**Concepts:** DISTINCT keyword

---

### 9. Find the cheapest product in the Electronics category
```sql
-- Expected Output: ProductName, Price, Category
```
**Concepts:** MIN() function, WHERE clause

---

### 10. Get all orders placed between 2025-05-10 and 2025-05-15
```sql
-- Expected Output: OrderID, UserID, OrderDate, TotalAmount
-- Should return 6 orders
```
**Concepts:** WHERE with date range (BETWEEN)

---

## <a id="intermediate"></a>🟡 INTERMEDIATE LEVEL - JOINs & GROUP BY

### 11. Show each order with customer name and order details
```sql
-- Expected Output: OrderID, UserName, OrderDate, TotalAmount, Status
-- Use INNER JOIN between Users and Orders
```
**Concepts:** INNER JOIN, joining 2 tables

---

### 12. List all products ordered by each customer
```sql
-- Expected Output: UserName, ProductName, Quantity, UnitPrice
-- Use multiple JOINs (Users → Orders → OrderItems → Products)
```
**Concepts:** Multiple INNER JOINs

---

### 13. Count total orders per customer
```sql
-- Expected Output: UserName, TotalOrders
-- Group by UserID
-- Expected: Some users have 3 orders, others have 1-2
```
**Concepts:** GROUP BY, COUNT()

---

### 14. Calculate total revenue generated per customer
```sql
-- Expected Output: UserName, TotalSpent, NumberOfOrders
-- Ordered by TotalSpent DESC
```
**Concepts:** GROUP BY, SUM(), JOIN

---

### 15. Find average order value per customer
```sql
-- Expected Output: UserName, AvgOrderValue, City
-- Ordered by AvgOrderValue DESC
```
**Concepts:** GROUP BY, AVG()

---

### 16. Show which products have been ordered and how many times
```sql
-- Expected Output: ProductName, TimesOrdered, TotalQuantitySold
-- Ordered by TotalQuantitySold DESC
```
**Concepts:** GROUP BY with product, COUNT(DISTINCT OrderID)

---

### 17. List all orders with their items (formatted display)
```sql
-- Expected Output:
-- OrderID | UserName | OrderDate | TotalItems | TotalAmount
-- Show total items and total amount per order
```
**Concepts:** JOIN with aggregation

---

### 18. Find customers who spent more than ₹50,000
```sql
-- Expected Output: UserName, City, TotalSpent
-- Use GROUP BY with HAVING clause
```
**Concepts:** GROUP BY, HAVING, SUM()

---

### 19. List all products that have never been ordered
```sql
-- Expected Output: ProductName, Category, Price, Stock
-- LEFT JOIN and WHERE to find unmatched
```
**Concepts:** LEFT JOIN, IS NULL

---

### 20. Show the order with the highest total amount and its items
```sql
-- Expected Output: OrderID, UserName, TotalAmount, ProductName, Quantity, UnitPrice
-- The order should be the one with maximum TotalAmount
```
**Concepts:** JOIN, MAX() with filtering

---

## <a id="advanced"></a>🔴 ADVANCED LEVEL - Subqueries & Complex Logic

### 21. Find customers who have placed orders above the average order value
```sql
-- Expected Output: UserName, OrderID, TotalAmount
-- Order value must be > overall average order value
-- Hint: Use subquery to calculate average first
```
**Concepts:** Subquery in WHERE clause, AVG()

---

### 22. List products ordered by customers from Delhi
```sql
-- Expected Output: ProductName, Category, Quantity, OrderDate
-- Show all products ordered by Users from Delhi city
```
**Concepts:** Subquery with IN clause

---

### 23. Find the most expensive product in each category
```sql
-- Expected Output: Category, ProductName, Price
-- Should return 2 rows: Electronics max and Fashion max
```
**Concepts:** GROUP BY with MAX(), Subquery or Window Function

---

### 24. Calculate the percentage of each product's sales relative to total sales
```sql
-- Expected Output: ProductName, TotalSold, TotalValue, PercentageOfTotal
-- Example: If 100 total units sold, product with 25 units = 25%
```
**Concepts:** Subquery for totals, CAST/DECIMAL for percentage

---

### 25. Find customers who have ordered every category of products
```sql
-- Expected Output: UserName, CategoriesOrdered
-- Should return customers who ordered both Electronics and Fashion
```
**Concepts:** GROUP BY with COUNT(DISTINCT), HAVING

---

### 26. Get the order details with a running total of customer spending
```sql
-- Expected Output: UserName, OrderID, OrderDate, TotalAmount, RunningTotal
-- Running total shows cumulative spending per customer
```
**Concepts:** Window functions (if available) or subquery

---

### 27. Find orders that contain products from multiple categories
```sql
-- Expected Output: OrderID, UserName, OrderDate, CategoriesInOrder
-- Example: Order with both Electronics and Fashion items
```
**Concepts:** GROUP BY with COUNT(DISTINCT)

---

### 28. List top 3 customers by number of orders
```sql
-- Expected Output: UserName, OrderCount, TotalSpent
-- Ordered by OrderCount DESC
```
**Concepts:** TOP with GROUP BY

---

### 29. Show products that sold more than the average quantity per product
```sql
-- Expected Output: ProductName, TotalQuantitySold, AvgQtyPerProduct
```
**Concepts:** GROUP BY, HAVING with AVG()

---

### 30. Find customers who haven't placed any orders (if exists in data)
```sql
-- Expected Output: UserName, Email, City
-- Use LEFT JOIN to find users with no orders
```
**Concepts:** LEFT JOIN with IS NULL

---

## <a id="expert"></a>💎 EXPERT LEVEL - Complex Queries & Optimization

### 31. Rank customers by total spending with tier classification
```sql
-- Expected Output: UserName, TotalSpent, Rank, Tier
-- Tier: "Premium" (top 30%), "Regular" (30-70%), "Basic" (bottom 30%)
```
**Concepts:** Window functions (RANK/ROW_NUMBER), CASE statement

---

### 32. Find the most profitable products considering both quantity and margin
```sql
-- Expected Output: ProductName, TotalRevenue, TotalCost (simulated), Profit
-- Assume cost is 60% of selling price
```
**Concepts:** Calculated fields, aggregation

---

### 33. Identify products that are trending (increasing orders over time)
```sql
-- Expected Output: ProductName, MayFirstWeek, MaySecondWeek, MayThirdWeek, Trend
-- Compare weekly order quantities
```
**Concepts:** Date functions, CASE statement, time-based grouping

---

### 34. Get the next purchase prediction for each customer
```sql
-- Expected Output: UserName, LastOrderDate, AvgDaysBetweenOrders, PredictedNextOrder
-- Calculate average days between orders and predict next
```
**Concepts:** DATEDIFF, AVG(), Date arithmetic

---

### 35. Create a customer segmentation query
```sql
-- Expected Output: UserName, OrderCount, AvgOrderValue, TotalSpent, Segment
-- Segment: High-Value (High spend + Frequent), Regular (Medium), At-Risk (Low activity)
```
**Concepts:** CASE statement with multiple conditions

---

### 36. Find the best-performing product for each month
```sql
-- Expected Output: Month, ProductName, OrderCount, Revenue
-- Top product by revenue for each month
```
**Concepts:** Date functions, GROUP BY with multiple fields, Window functions

---

### 37. Calculate customer lifetime value with historical analysis
```sql
-- Expected Output: UserName, FirstOrderDate, LastOrderDate, MonthsActive, 
--                  TotalOrders, TotalSpent, AvgMonthlyValue, CLV
```
**Concepts:** Date calculations, aggregate functions

---

### 38. Inventory impact analysis - products that need restocking
```sql
-- Expected Output: ProductName, CurrentStock, MonthlyDemand, MonthsUntilStockout
-- Calculate if product will run out and when
```
**Concepts:** Subquery for monthly demand, division, case logic

---

### 39. Build a product recommendations engine (customers who bought X also bought Y)
```sql
-- Expected Output: ProductName, RecommendedProducts, FrequencyOfTogether
-- For each product, show what else is frequently bought with it
```
**Concepts:** Self JOIN, GROUP BY, multiple aggregations

---

### 40. Create an anomaly detection query for unusual order patterns
```sql
-- Expected Output: OrderID, UserName, TotalAmount, AvgOrderAmount, Variance, IsAnomaly
-- Flag orders that deviate significantly from user's average
```
**Concepts:** Subquery for averages, CASE statement, statistical functions

---

## <a id="challenges"></a>🏆 CHALLENGE PROBLEMS

### Challenge 1: Complete Sales Dashboard Query
```
Create a single query that returns:
- UserName
- NumberOfOrders
- TotalSpent
- AvgOrderValue
- MostExpensiveOrder
- FavoriteCategory
- LastOrderDate
- Days Since Last Order

Use appropriate JOINs and aggregations.
```

---

### Challenge 2: Order Fulfillment Analysis
```
Write a query to analyze order fulfillment:
- OrderID
- UserName
- OrderDate
- Status
- ItemCount
- TotalValue
- DaysToFulfill (estimated: 3 days for Pending, 1 for Shipped, 0 for Delivered)
- OnTimePercentage (across all customer's orders)

Group results by fulfillment status.
```

---

### Challenge 3: Competitive Market Analysis
```
Create a query comparing:
- Category
- TotalProducts
- AvgPrice
- MaxPrice
- MinPrice
- TotalUnitsSold
- TotalRevenue
- AvgRevenuePerProduct

Identify which category is most profitable.
```

---

### Challenge 4: Customer Journey Timeline
```
Build a chronological query showing:
- UserName
- OrderSequence (1st order, 2nd order, etc.)
- OrderDate
- TotalAmount
- DaysSincePreviousOrder
- CategoryOrdered
- CumulativeSpending
- IsReturningCustomer (ordered more than once)
```

---

### Challenge 5: Predictive Stock Management Query
```
Create a comprehensive inventory query:
- ProductName
- Category
- CurrentStock
- MonthlyConsumption (from order data)
- StockTurnoverRate
- MonthsOfStockRemaining
- ReorderLevel (recommended: 3 months supply)
- Action (Urgent Reorder, Standard Order, Adequate)
- EstimatedRevenueLoss if out of stock

Identify critical products.
```

---

## 🎯 ANSWER KEY STRUCTURE

For each question, expected results should include:
- **Number of rows** returned
- **Column names** and data types
- **Sample values** from result set
- **Execution notes** (any special considerations)

---

## 📊 DIFFICULTY PROGRESSION

```
Beginner (Q1-10)      → SELECT, WHERE, ORDER BY, DISTINCT, Basic Functions
                       Est. Time: 5-10 mins per question

Intermediate (Q11-20) → JOINs, GROUP BY, HAVING, Aggregate Functions
                       Est. Time: 15-25 mins per question

Advanced (Q21-30)     → Subqueries, Complex Joins, Window Functions
                       Est. Time: 20-30 mins per question

Expert (Q31-40)       → Complex Logic, Optimization, Statistical Functions
                       Est. Time: 30-45 mins per question

Challenges (C1-5)     → Real-world Scenarios, Multiple Concepts Combined
                       Est. Time: 45-60 mins per challenge
```

---

## 💡 LEARNING TIPS

1. **Start with Beginner questions** - Build confidence with basic syntax
2. **Write queries without looking at hints** - Then check solutions
3. **Try different approaches** - Multiple ways to solve the same problem
4. **Optimize as you go** - Better joins, index awareness
5. **Test with sample data first** - Verify logic before complex datasets
6. **Document your queries** - Add comments explaining logic
7. **Compare your results** - Check row counts match expectations

---

## 🔧 SQL CONCEPTS CHECKLIST

**Master these to answer all questions:**

- [ ] Basic SELECT statements
- [ ] WHERE clause with AND/OR/NOT
- [ ] Comparison operators (>, <, =, !=, BETWEEN, IN)
- [ ] LIKE pattern matching
- [ ] ORDER BY (ASC/DESC)
- [ ] DISTINCT keyword
- [ ] LIMIT/TOP for row limiting
- [ ] Aggregate functions (COUNT, SUM, AVG, MIN, MAX)
- [ ] GROUP BY clause
- [ ] HAVING clause
- [ ] INNER JOIN
- [ ] LEFT JOIN / RIGHT JOIN
- [ ] FULL OUTER JOIN
- [ ] Multiple JOINs
- [ ] Subqueries (WHERE, FROM, SELECT)
- [ ] Correlated subqueries
- [ ] CASE statements
- [ ] Date functions (DATEDIFF, DATEADD, MONTH, YEAR)
- [ ] String functions (CONCAT, SUBSTRING, UPPER, LOWER)
- [ ] Numeric functions (CAST, CONVERT, ROUND)
- [ ] Window functions (ROW_NUMBER, RANK, DENSE_RANK)
- [ ] Common Table Expressions (CTE) - WITH clause
- [ ] Unions and Intersects

---

## 📝 NEXT STEPS

1. **Copy the database schema** from the main document
2. **Create the tables and insert data**
3. **Start with Beginner questions** (Q1-Q10)
4. **Move progressively through levels**
5. **Attempt Challenges** after mastering all levels
6. **Compare solutions** and optimize your queries

---

**Happy Learning! 🚀 Master SQL with real-world scenarios!**
