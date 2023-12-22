# SQL_brainchamp

## Download configuration files for PostgreSQL database setup(PDADMIN)

Google search - postgresql download

Hit postgresql.org

Download the windows installer

Launch the installer, give it a password and a port number.

Note that this postgresql installation comes with PGADMIN as well.

Now after the installation, hit start and search postgresql documentation, find the PDADMIN icon.

Open PGADMIN and left click on database to create a new database.

Left click on login/group role to create new permissions.

Now left click on the database and click on 'query tool' to query your new database.


## Create tables

### Customer Table
```
-- Customers Table
CREATE TABLE Customers (
    CustomerID SERIAL PRIMARY KEY,
    Name VARCHAR(100),
    Email VARCHAR(100),
    Country VARCHAR(50)
);
```

```
-- Inserting Data into Customers Table
INSERT INTO Customers (Name, Email, Country) VALUES
('John Doe', 'johndoe@email.com', 'USA'),
('Jane Smith', 'janesmith@email.com', 'UK'),
('Alice Johnson', 'alicej@email.com', 'Canada'),
('Chris Green', 'chrisg@email.com', 'USA'),
('Emma Brown', 'emmab@email.com', 'UK'),
('Liam Miller', 'liamm@email.com', 'Canada'),
('Olivia Davis', 'oliviad@email.com', 'USA'),
('James Wilson', 'jamesw@email.com', 'UK'),
('Isabella Taylor', 'isabellat@email.com', 'Canada'),
('Michael Anderson', 'michaela@email.com', 'USA');

```


### Product table

```
-- Products Table
CREATE TABLE Products (
    ProductID SERIAL PRIMARY KEY,
    Name VARCHAR(100),
    Price DECIMAL(10, 2),
    Category VARCHAR(50)
);
```

```
-- Inserting Data into Products Table
INSERT INTO Products (Name, Price, Category) VALUES
('Laptop', 1200.00, 'Electronics'),
('Smartphone', 800.00, 'Electronics'),
('Headphones', 150.00, 'Electronics'),
('Book "SQL Essentials"', 20.00, 'Books'),
('Gaming Console', 500.00, 'Electronics'),
('Backpack', 70.00, 'Accessories'),
('Desk Lamp', 30.00, 'Home Decor'),
('Wall Clock', 25.00, 'Home Decor'),
('Yoga Mat', 40.00, 'Fitness'),
('Water Bottle', 15.00, 'Fitness');

```


### Orders table

```
-- Orders Table
CREATE TABLE Orders (
    OrderID SERIAL PRIMARY KEY,
    CustomerID INT REFERENCES Customers(CustomerID),
    OrderDate DATE,
    TotalAmount DECIMAL(10, 2)
);
```

```
-- Inserting Data into Orders Table
INSERT INTO Orders (CustomerID, OrderDate, TotalAmount) VALUES
(1, '2023-12-01', 2000.00),
(2, '2023-12-02', 1600.00),
(3, '2023-12-03', 1200.00),
(4, '2023-12-04', 500.00),
(5, '2023-12-05', 600.00),
(6, '2023-12-06', 700.00),
(7, '2023-12-07', 400.00),
(8, '2023-12-08', 800.00),
(9, '2023-12-09', 300.00),
(10, '2023-12-10', 900.00);
```


### OrderDetails Table

```
-- OrderDetails Table
CREATE TABLE OrderDetails (
    OrderDetailID SERIAL PRIMARY KEY,
    OrderID INT REFERENCES Orders(OrderID),
    ProductID INT REFERENCES Products(ProductID),
    Quantity INT,
    LineTotal DECIMAL(10, 2)
);
```

```
-- Inserting Data into OrderDetails Table
INSERT INTO OrderDetails (OrderID, ProductID, Quantity, LineTotal) VALUES
(1, 1, 1, 1200.00),
(1, 2, 1, 800.00),
(2, 3, 2, 300.00),
(3, 4, 3, 60.00),
(4, 5, 1, 500.00),
(5, 6, 2, 140.00),
(6, 7, 3, 90.00),
(7, 8, 2, 50.00),
(8, 9, 1, 40.00),
(9, 10, 3, 45.00),
(10, 1, 1, 1200.00);
```





# PostgreSQL Syntax


## 1 SELECT

Use Case: To retrieve customer details.

```
SELECT * FROM Customers;
```


## 2 SELECT DISTINCT

Use Case: List distinct categories of products.

```
SELECT DISTINCT Category FROM Products;
```


## 3 MIN and MAX

Use Case: Find the cheapest and most expensive product prices.

```
SELECT MIN(Price) AS CheapestProductPrice, MAX(Price) AS MostExpensiveProductPrice FROM Products;
```


## 4 ORDER BY

Use Case: Sort products by price in ascending order.

```
SELECT * FROM Products ORDER BY Price ASC;
```


## 5 

Use Case: Count the total number of orders made.

```
SELECT COUNT(*) AS TotalOrders FROM Orders;
```

## 6 SUM

Use Case: Calculate the total revenue from all orders.

```
SELECT SUM(TotalAmount) AS TotalRevenue FROM Orders;
```

## 7 INNER JOIN

Use Case: View all orders along with customer names.

```
SELECT Customers.Name, Orders.OrderID, Orders.TotalAmount
FROM Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID;
```


## 8 LEFT JOIN

Use Case: List all customers and their orders, including those who haven't made any orders.

```
SELECT Customers.Name, Orders.OrderID
FROM Customers
LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```


## 9 RIGHT JOIN

Use Case: List all orders, including those not linked to a customer in the database.

```
SELECT Orders.OrderID, Customers.Name
FROM Orders
RIGHT JOIN Customers ON Orders.CustomerID = Customers.CustomerID;
```


## 10 FULL JOIN

Use Case: Combine and list all records from both Customers and Orders tables.

```
SELECT Customers.Name, Orders.OrderID
FROM Customers
FULL JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```


