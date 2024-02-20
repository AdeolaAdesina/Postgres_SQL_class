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


##Step 2: Creating the Schema in PostgreSQL

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


