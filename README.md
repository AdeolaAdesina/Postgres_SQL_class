# Postgres_SQL_class


## Step 1: Designing the Tables
Customers

- CustomerID (Primary Key)
- Name
- Email
- Address
- City
- Province
- PostalCode

Products

- ProductID (Primary Key)
- Name
- Description
- Price
- CategoryID (Foreign Key)

Categories

- CategoryID (Primary Key)
- CategoryName

Orders

- OrderID (Primary Key)
- CustomerID (Foreign Key)
- OrderDate
- Status

OrderDetails

- OrderDetailID (Primary Key)
- OrderID (Foreign Key)
- ProductID (Foreign Key)
- Quantity
- Price


## Step 2: Creating the Schema in PostgreSQL

Below are the SQL statements to create these tables in a PostgreSQL database, including primary keys, foreign keys, and some basic constraints like NOT NULL for essential fields.


Create "Customers" table

```
CREATE TABLE Customers (
    CustomerID SERIAL PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Email VARCHAR(100) UNIQUE NOT NULL,
    Address VARCHAR(255) NOT NULL,
    City VARCHAR(50) NOT NULL,
    Province VARCHAR(50) NOT NULL,
    PostalCode VARCHAR(7) NOT NULL
);
```

Create "Categories" table

```
CREATE TABLE Categories (
    CategoryID SERIAL PRIMARY KEY,
    CategoryName VARCHAR(50) NOT NULL
);
```

Create "Products" table

```
CREATE TABLE Products (
    ProductID SERIAL PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Description TEXT,
    Price DECIMAL(10, 2) NOT NULL CHECK (Price > 0),
    CategoryID INT NOT NULL,
    FOREIGN KEY (CategoryID) REFERENCES Categories(CategoryID)
);
```

Create "Orders" table

```
CREATE TABLE Orders (
    OrderID SERIAL PRIMARY KEY,
    CustomerID INT NOT NULL,
    OrderDate DATE NOT NULL,
    Status VARCHAR(50) NOT NULL,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```


Create "OrderDetails" table

```
CREATE TABLE OrderDetails (
    OrderDetailID SERIAL PRIMARY KEY,
    OrderID INT NOT NULL,
    ProductID INT NOT NULL,
    Quantity INT NOT NULL CHECK (Quantity > 0),
    Price DECIMAL(10, 2) NOT NULL CHECK (Price > 0),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID),
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
);
```


## Step 3: Inserting Sample Data into the Tables


Here are some sample INSERT statements for each table. 

Insert data into "Customers"

```
INSERT INTO Customers (Name, Email, Address, City, Province, PostalCode) VALUES
('John Doe', 'johndoe@example.com', '123 Elm St', 'Toronto', 'Ontario', 'M4B 1B3'),
('Jane Smith', 'janesmith@example.com', '456 Maple Ave', 'Vancouver', 'British Columbia', 'V5K 0A1'),
('Ahmed Khan', 'ahmedkhan@example.com', '789 Pine Rd', 'Calgary', 'Alberta', 'T2P 2M2'),
('Maria Garcia', 'mariagarcia@example.com', '321 Oak Ln', 'Montreal', 'Quebec', 'H3Z 2Y7'),
('Chen Wei', 'chenwei@example.com', '654 Spruce Ct', 'Ottawa', 'Ontario', 'K1A 0B1'),
('Emily Johnson', 'emilyjohnson@example.com', '987 Cedar Pl', 'Mississauga', 'Ontario', 'L5G 2T6'),
('Carlos Hernandez', 'carloshernandez@example.com', '123 Birch St', 'Winnipeg', 'Manitoba', 'R3J 0X9'),
('Aisha Patel', 'aishapatel@example.com', '456 Alder Rd', 'Saskatoon', 'Saskatchewan', 'S7N 1K4'),
('Alexander Smith', 'alexandersmith@example.com', '789 Willow Ave', 'Halifax', 'Nova Scotia', 'B3H 2Z6'),
('Sophia Brown', 'sophiabrown@example.com', '321 Elm Pl', 'Quebec City', 'Quebec', 'G1V 3V4');
```


Insert data into "Categories"

```
INSERT INTO Categories (CategoryName) VALUES
('Electronics'),
('Books'),
('Home & Garden'),
('Toys & Games'),
('Clothing'),
('Health & Beauty'),
('Sports & Outdoors'),
('Pet Supplies'),
('Food & Grocery'),
('Automotive');
```

Insert data into "Products"

INSERT INTO Products (Name, Description, Price, CategoryID) VALUES
('Laptop', 'A high-performance laptop.', 1200.00, 1),
('Database Management Book', 'A comprehensive guide to database management.', 45.00, 2),
('Garden Shovel', 'Durable shovel for gardening.', 22.95, 3),
('Board Game', 'Fun for the whole family.', 35.00, 4),
('Men\'s T-shirt', '100% cotton, size medium.', 19.99, 5),
('Shampoo', 'Organic and natural hair care.', 12.50, 6),
('Camping Tent', 'Two-person tent, waterproof.', 89.99, 7),
('Dog Leash', 'Strong and durable leash for dogs.', 9.99, 8),
('Organic Almonds', 'Raw organic almonds, 1lb.', 15.99, 9),
('Car Wax', 'High-quality wax for car care.', 23.99, 10);


Insert data into "Orders"

```
-- Assuming a simple pattern for OrderDate for illustration; in practice, these would vary more.
INSERT INTO Orders (CustomerID, OrderDate, Status) VALUES
(1, '2024-02-20', 'Shipped'),
(2, '2024-02-21', 'Processing'),
(3, '2024-02-22', 'Delivered'),
(4, '2024-02-23', 'Shipped'),
(5, '2024-02-24', 'Processing'),
(6, '2024-02-25', 'Delivered'),
(7, '2024-02-26', 'Shipped'),
(8, '2024-02-27', 'Processing'),
(9, '2024-02-28', 'Delivered'),
(10, '2024-02-29', 'Shipped');
```


Insert data into "OrderDetails"

```
-- Sample data with some arbitrary quantities and prices for simplicity.
INSERT INTO OrderDetails (OrderID, ProductID, Quantity, Price) VALUES
(1, 1, 1, 1200.00),
(2, 2, 2, 90.00),
(3, 3, 1, 22.95),
(4, 4, 3, 105.00),
(5, 5, 2, 39.98),
(6, 6, 4, 50.00),
(7, 7, 1, 89.99),
(8, 8, 2, 19.98),
(9, 9, 3, 47.97),
(10, 10, 1, 23.99),
(1, 2, 1, 45.00),
(2, 3, 2, 45.90),
(3, 4, 1, 35.00),
(4, 5, 3, 59.97),
(5, 6, 2, 25.00),
(6, 7, 1, 89.99),
(7, 8, 2, 19.98),
(8, 9, 3, 47.97),
(9, 10, 1, 23.99),
(10, 1, 2, 2400.00);
```


## Step 4: SQL syntax.

1. Postgres Operators
Use Case: Find products priced over $50 to identify premium offerings.

```
SELECT Name, Price FROM Products WHERE Price > 50;
```

- =	Equal to
- ```<```	Less than
- ```>```	Greater than
- ```<=```	Less than or equal to
- ```>=```	Greater than or equal to
- ```<>```	Not equal to
- !=	Not equal to
- LIKE	Check if a value matches a pattern (case sensitive)
- ILIKE	Check if a value matches a pattern (case insensitive)
- AND	Logical AND
- OR	Logical OR
- IN	Check if a value is between a range of values
- BETWEEN	Check if a value is between a range of values
- IS NULL	Check if a value is NULL
- NOT	Makes a negative result e.g. NOT LIKE, NOT IN, NOT BETWEEN


2. SELECT
   
Use Case: Retrieve the names of all customers.

```
SELECT Name FROM Customers;
```


3. SELECT DISTINCT

Use Case: List all unique cities where customers are located to plan regional marketing campaigns.


```
SELECT DISTINCT City FROM Customers;
```

4. WHERE

Use Case: Identify orders that have been shipped for targeted follow-up surveys.


```
SELECT OrderID FROM Orders WHERE Status = 'Shipped';
```

5. ORDER BY

Use Case: Rank products by price in descending order to find the most expensive items sold.

```
SELECT Name, Price FROM Products ORDER BY Price DESC;
```


6. GROUP BY

Use Case: Count the number of orders by status to assess the operational workload.

```
SELECT Status, COUNT(*) FROM Orders GROUP BY Status;
```

7. LIMIT

Use Case: Get the top 5 most recent orders to quickly review the latest sales activity.

```
SELECT OrderID, OrderDate FROM Orders ORDER BY OrderDate DESC LIMIT 5;
```


8. MIN and MAX
Use Case: Determine the price range of products to understand the inventory's price diversity.

```
SELECT MIN(Price) AS MinPrice, MAX(Price) AS MaxPrice FROM Products;
```


9. COUNT
Use Case: Find out how many products are available in each category for stock level analysis.

```
SELECT CategoryID, COUNT(*) FROM Products GROUP BY CategoryID;
```


10. SUM and AVERAGE
Use Case: Calculate the total sales and average sales per order to gauge performance.

```
SELECT SUM(Price * Quantity) AS TotalSales, AVG(Price * Quantity) AS AverageSale FROM OrderDetails;
```


11. LIKE
Use Case: Search for products with 'laptop' in their name to analyze the electronics category.

```
SELECT Name FROM Products WHERE Name LIKE '%laptop%';
```


12. IN
Use Case: Select orders from either Toronto or Vancouver to focus on urban customer bases.

```
SELECT OrderID FROM Orders JOIN Customers ON Orders.CustomerID = Customers.CustomerID WHERE City IN ('Toronto', 'Vancouver');
```


13. BETWEEN
Use Case: Identify products priced between $10 and $100 for a mid-range product promotion.

```
SELECT Name, Price FROM Products WHERE Price BETWEEN 10 AND 100;
```


14. AS (Alias)
Use Case: Simplify column names in the output of a query that calculates total sales per order for readability.

```
SELECT OrderID, SUM(Price * Quantity) AS TotalSale FROM OrderDetails GROUP BY OrderID;
```

15. Joins and Types

INNER JOIN
Use Case: Match products to their categories to list what items belong to 'Electronics'.


```
SELECT Products.Name FROM Products INNER JOIN Categories ON Products.CategoryID = Categories.CategoryID WHERE Categories.CategoryName = 'Electronics';
```

LEFT JOIN

Use Case: List all customers and their orders, including those who haven't made any orders.

```
SELECT Customers.Name, Orders.OrderID FROM Customers LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```

RIGHT JOIN
Use Case: Ensure all orders, even those mistakenly not linked to a customer, are accounted for in audit logs.

```
SELECT Customers.Name, Orders.OrderID FROM Customers RIGHT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```

FULL JOIN
Use Case: Combine LEFT JOIN and RIGHT JOIN use cases to get a complete picture of orders and customers, including mismatches.

```
SELECT Customers.Name, Orders.OrderID FROM Customers FULL JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```

16. UNION
Use Case: Create a combined list of all city names from both customers and suppliers (assuming a suppliers table exists).

```
SELECT City FROM Customers UNION SELECT City FROM Suppliers;
```

17. Statistics (Mean, Median, Mode)
Mean (Average): Already covered under SUM and AVERAGE.
Median: PostgreSQL does not have a built-in function for median, but you can use percentile_cont.
Mode: You can use the mode() within a SELECT statement with the OVER() window function for grouped categories.

Use Case for Median: Find the median sales price across all orders.

```
SELECT percentile_cont(0.5) WITHIN GROUP (ORDER BY Price) AS MedianPrice FROM OrderDetails;
```


Use Case for Mode: Determine the most common quantity ordered for all products.

```
SELECT mode() WITHIN GROUP (ORDER BY Quantity) FROM OrderDetails;
```


18. Remove NULL Values
Use Case: List all products, including their category names, ensuring no NULL values in the category name for clean data analysis.


```
SELECT Products.Name, Categories.CategoryName FROM Products JOIN Categories ON Products.CategoryID = Categories.CategoryID WHERE Categories.CategoryName IS NOT NULL;
```

19. Understanding CTEs

A Common Table Expression (CTE) provides a way to create a temporary result set that you can reference within a SELECT, INSERT, UPDATE, or DELETE statement. CTEs are particularly useful for breaking down complex queries into simpler parts.

Example: Customer Retention Analysis
Objective Simplified: Identify customers who have made more than 1 order.

Let's break this down into a simpler CTE example:


```
WITH CustomerOrderCounts AS (
  SELECT 
    CustomerID, 
    COUNT(OrderID) AS NumberOfOrders
  FROM Orders
  GROUP BY CustomerID
)
SELECT 
  CustomerID
FROM CustomerOrderCounts
WHERE NumberOfOrders > 1;
```

Breakdown:

CTE Definition: The WITH clause starts the CTE, naming it CustomerOrderCounts. This CTE selects the CustomerID from the Orders table and counts how many orders each customer has made.

CTE Usage: After defining the CTE, the main query (SELECT CustomerID FROM CustomerOrderCounts WHERE NumberOfOrders > 1) uses the result set of the CTE to find customers who have made more than 1 order.


Understanding Subqueries
A subquery is a query nested inside another query. It can be used in various places, including the SELECT, FROM, and WHERE clauses of the main query.

Example: Find Products with Above Average Price
Objective Simplified: List all products that have a price above the average price of all products.

```
SELECT Name, Price
FROM Products
WHERE Price > (
  SELECT AVG(Price) FROM Products
);
```


Breakdown:

Subquery: The subquery (SELECT AVG(Price) FROM Products) calculates the average price of all products in the Products table.

Main Query: The main query selects the name and price of products from the Products table where the product's price is greater than the average price calculated by the subquery.


- Combining CTEs and Subqueries
Now, let's slightly increase the complexity by combining a CTE with a subquery.

Example: Customers with Above Average Orders
Objective: Identify customers who have made a number of orders above the average, using both a CTE and a subquery.

```
WITH CustomerOrderCounts AS (
  SELECT 
    CustomerID, 
    COUNT(OrderID) AS NumberOfOrders
  FROM Orders
  GROUP BY CustomerID
)
SELECT 
  CustomerID
FROM CustomerOrderCounts
WHERE NumberOfOrders > (
  SELECT AVG(NumberOfOrders) FROM CustomerOrderCounts
);
```


Breakdown:

CTE (CustomerOrderCounts): This CTE calculates the number of orders each customer has made.

Subquery in WHERE Clause: The subquery (SELECT AVG(NumberOfOrders) FROM CustomerOrderCounts) calculates the average number of orders made by all customers.
Main Query with CTE and Subquery: The main query then selects customers from the CustomerOrderCounts CTE whose number of orders is greater than this average.

By breaking down complex queries into smaller, more manageable parts, both CTEs and subqueries help improve the readability and maintainability of SQL code, making it easier to understand and debug. This step-by-step approach allows you to tackle more complex data analysis tasks by building on simpler concepts.



# Approach to solving problems in SQL

- Always understand all the tables in the database.
- Always understand the relationships between all the tables.
- Identify the tables needed to solve a particular problem
- Figure out what field in each table is needed for analysis
- Figure out if you need a simple query, a CTE or Sub-query



# Business Problem 1: Customer Retention Analysis

Objective: Identify customers who have made more than the average number of orders but have a total spending less than the average. This could indicate customers who are frequent buyers but spend less, possibly targeting them with promotions to increase their basket size.


# Business Problem 2: Inventory Management

Objective: Find the top 5 most popular products in each category based on quantity sold, to inform inventory restocking decisions. Products with higher sales volumes should be prioritized for restocking.


# Business Problem 3: Marketing Campaign Effectiveness

Objective: Generate a monthly sales report showing the total number of orders and total sales for each month. This report will help the business understand monthly sales trends and identify months with high sales volume.
