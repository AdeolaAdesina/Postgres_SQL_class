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
