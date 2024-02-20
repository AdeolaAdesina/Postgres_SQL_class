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


