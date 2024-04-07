# Database Usage Guide
This guide provides comprehensive instructions for using the **Inventory and Streamline Order Processing database system**, including schema setup, data insertion, executing basic and advanced 
queries, and leveraging views, functions, and stored procedures.

## Schema Setup
### Creating Schema and Tables
First, connect to the database and execute the following SQL commands to set up the schema and create tables:
```sql
-- Create the necessary schema (database)
CREATE DATABASE IF NOT EXISTS inventoryandstreamlineorderprocessingreducedby20percent;

-- Switch to the created schema
USE inventoryandstreamlineorderprocessingreducedby20percent;

-- Table for Products
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(255) NOT NULL,
    Description TEXT,
    Price DECIMAL(10, 2) NOT NULL
);

-- Table for Inventory
CREATE TABLE Inventory (
    ProductID INT,
    Quantity INT,
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
);

-- Table for Customers
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    FirstName VARCHAR(45) NOT NULL,
    LastName VARCHAR(45) NOT NULL,
    Email VARCHAR(45) NOT NULL
);

-- Table for Orders
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATETIME DEFAULT CURRENT_TIMESTAMP,
    TotalAmount DECIMAL(10, 2),
    Status VARCHAR(45),
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);

-- Table for Order Details
CREATE TABLE OrderDetails (
    OrderDetailID INT PRIMARY KEY,
    OrderID INT,
    ProductID INT,
    Quantity INT,
    Price DECIMAL(10, 2),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID),
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
);
```
## Data Insertion
Now, insert data into the tables to populate the database with initial records:
```sql
INSERT INTO Product (ProductID, ProductName, Description, Price) VALUES 
    (1, 'Laptop', 'High-performance laptop with SSD storage', 999.99),
    (2, 'Smartphone', 'Latest smartphone with advanced features', 699.99),
    (3, 'Tablet', 'Portable tablet with high-resolution display', 299.99),
    (4, 'Headphones', 'Wireless headphones with noise-cancellation', 199.99),
    (5, 'Smartwatch', 'Fitness tracker with heart rate monitor', 149.99),
    (6, 'Bluetooth Speaker', 'Portable speaker with Bluetooth connectivity', 79.99),
    (7, 'External Hard Drive', 'High-capacity external hard drive for data storage', 129.99),
    (8, 'Wireless Mouse', 'Ergonomic wireless mouse for improved productivity', 29.99),
    (9, 'Gaming Keyboard', 'Mechanical gaming keyboard with RGB lighting', 149.99),
    (10, 'Graphic Tablet', 'Digital drawing tablet for artists and designers', 199.99),
    (11, 'Wireless Router', 'High-speed wireless router for home network', 89.99),
    (12, 'Portable SSD', 'Compact solid-state drive for fast data transfer', 179.99),
    (13, 'Fitness Tracker', 'Activity tracker with step counter and sleep monitor', 49.99),
    (14, 'Digital Camera', 'High-resolution digital camera for photography enthusiasts', 399.99),
    (15, 'Desktop Monitor', 'Ultra-wide monitor for immersive gaming and productivity', 599.99),
    (16, 'USB Flash Drive', 'Portable USB flash drive for data storage and transfer', 19.99),
    (17, 'Wireless Earbuds', 'True wireless earbuds with long battery life', 129.99),
    (18, 'Webcam', 'HD webcam for video conferencing and streaming', 69.99),
    (19, 'Printer', 'All-in-one printer for printing, scanning, and copying', 149.99),
    (20, 'Wireless Keyboard', 'Slim wireless keyboard for comfortable typing', 49.99);
    
-- Inserting customers
INSERT INTO Customers (CustomerID, FirstName, LastName, Email)
VALUES (1, 'John', 'Doe', 'john.doe@example.com'),
       (2, 'Jane', 'Smith', 'jane.smith@example.com'),
       (3, 'Michael', 'Johnson', 'michael.johnson@example.com'),
       (4, 'Emily', 'Brown', 'emily.brown@example.com'),
       (5, 'William', 'Jones', 'william.jones@example.com');
       
-- Inserting inventory information for 10 products
INSERT INTO Inventory (ProductID, Quantity) VALUES 
    (1, 100),   -- ProductID 1 with quantity 100
    (2, 150),   -- ProductID 2 with quantity 150
    (3, 200),   -- ProductID 3 with quantity 200
    (4, 80),    -- ProductID 4 with quantity 80
    (5, 120),   -- ProductID 5 with quantity 120
    (6, 90),    -- ProductID 6 with quantity 90
    (7, 180),   -- ProductID 7 with quantity 180
    (8, 70),    -- ProductID 8 with quantity 70
    (9, 110),   -- ProductID 9 with quantity 110
    (10, 160);  -- ProductID 10 with quantity 160

-- Inserting a new order
INSERT INTO Orders (OrderID, CustomerID, TotalAmount, Status)
VALUES (1, 1, 1699.98, 'Pending');

INSERT INTO Orders (OrderID, CustomerID, OrderDate, TotalAmount, Status)
VALUES (1, 1, CURRENT_TIMESTAMP, 1699.98, 'Pending');

-- Inserting additional orders
INSERT INTO Orders (OrderID, CustomerID, OrderDate, TotalAmount, Status)
VALUES (2, 2, '2024-03-04', 1299.99, 'Pending'),  -- Order for customer with CustomerID 2
       (3, 3, '2024-03-05', 899.99, 'Pending'),  -- Order for customer with CustomerID 3
       (4, 1, '2024-03-06', 1599.99, 'Shipped'), -- Order for customer with CustomerID 1
       (5, 4, '2024-03-07', 799.99, 'Pending');  -- Order for customer with CustomerID 4

-- Inserting order details
INSERT INTO OrderDetails (OrderDetailID, OrderID, ProductID, Quantity, Price)
VALUES (1, 1, 1, 1, 999.99), -- Laptop
       (2, 1, 2, 1, 699.99); -- Smartphone
```
## Basic Queries
Execute basic SQL queries to retrieve data from the database:

```sql
-- Retrieve all products
SELECT * FROM Products;

-- Retrieve all order details
SELECT * FROM OrderDetails;

-- Retrieve inventory information
SELECT * FROM Inventory;

-- Retrieve all orders
SELECT * FROM Orders;

-- Retrieve all customers
SELECT * FROM Customers;
```

## Advanced Queries
Execute advanced SQL queries to perform data analysis and reporting:

```sql
-- Retrieve Orders for a Specific Customer (e.g., CustomerID = 3)
SELECT * FROM Orders WHERE CustomerID = 3;
```
```sql
-- Calculate Total Sales for Each Product
SELECT 
    ProductID,
    SUM(Quantity) AS TotalQuantity,
    SUM(Price * Quantity) AS TotalSales
FROM OrderDetails
GROUP BY ProductID;
```
```sql
-- Update Order Status to 'Shipped' for a specific OrderID (e.g., OrderID = 1)
UPDATE Orders
SET Status = 'Shipped'
WHERE OrderID = 1;
```
```sql
-- Retrieve Product Information with Current Inventory Levels
SELECT 
    p.ProductID,
    p.ProductName,
    p.Description,
    p.Price,
    i.Quantity
FROM Products p
INNER JOIN Inventory i ON p.ProductID = i.ProductID;
```
## Views, Functions, and Stored Procedures
Create views, functions, and stored procedures to simplify complex operations and enhance database functionality:

```sql
-- Create a view to retrieve order details along with product information
CREATE VIEW OrderProductDetails AS
SELECT o.OrderID, o.OrderDate, o.CustomerID,
       od.ProductID, od.Quantity, od.Price,
       p.ProductName, p.Description
FROM Orders o
JOIN OrderDetails od ON o.OrderID = od.OrderID
JOIN Products p ON od.ProductID = p.ProductID;
```
```sql
-- Create a stored procedure to calculate total price for a given product and quantity
DELIMITER //
CREATE PROCEDURE CalculateTotalPrice (
    IN product_id INT,
    IN quantity INT,
    OUT total_price DECIMAL(10, 2)
)
BEGIN
    SELECT Price * quantity INTO total_price
    FROM Products
    WHERE ProductID = product_id;
END//
DELIMITER ;
```
```sql
-- Create a stored procedure to place an order
DELIMITER //
CREATE PROCEDURE PlaceOrder (
    IN customer_id INT,
    IN product_id INT,
    IN quantity INT
)
BEGIN
    DECLARE total_price DECIMAL(10, 2);
    DECLARE new_order_id INT;

    -- Calculate total price
    CALL CalculateTotalPrice(product_id, quantity, total_price);

    -- Insert into Orders table
    INSERT INTO Orders (CustomerID, TotalAmount, Status)
    VALUES (customer_id, total_price, 'Pending');

    -- Get the OrderID of the newly inserted order
    SELECT LAST_INSERT_ID() INTO new_order_id;

    -- Insert into OrderDetails table
    INSERT INTO OrderDetails (OrderID, ProductID, Quantity, Price)
    VALUES (new_order_id, product_id, quantity, total_price);

    -- Update Inventory
    UPDATE Inventory
    SET Quantity = Quantity - quantity
    WHERE ProductID = product_id;
END //
DELIMITER ;
```
To demonstrate the usage of views and stored procedures in the context of the **Inventory and Streamline Order Processing database system**, we will showcase how to interact with the 
created views and execute the defined stored procedures.

### Using Views
A view in a database is a virtual table generated from the result set of a SELECT query. It provides a way to simplify complex queries and encapsulate specific data retrieval logic. 
In our database, we have created a view called **`OrderProductDetails`** to retrieve order details along with associated product information.

Retrieving Data Using a View
To retrieve data from the **`OrderProductDetails view`**, you can simply execute a SELECT query against this view:

```sql
-- Retrieve order details along with product information using the view
SELECT * FROM OrderProductDetails;
```
This query will return a combined result of order details and associated product information based on the defined view's logic.

### Using Stored Procedures
A stored procedure is a set of SQL statements that can be stored and executed as a single unit. It helps in encapsulating business logic and allows for code reuse and modularity. 
In our database, we have defined a stored procedure named **`PlaceOrder`** to facilitate the process of placing an order, which involves calculating the total price, inserting records into 
the **`Orders`** and **`OrderDetails`** tables, and updating the inventory.

Executing a Stored Procedure
To execute the PlaceOrder stored procedure and place a new order, you need to call the procedure with appropriate parameters:

```sql
-- Example: Place an order for CustomerID 1 with ProductID 3 and Quantity 2
CALL PlaceOrder(1, 3, 2);
```
In this example:

- 1 is the **`customer_id`** representing the CustomerID.
- 3 is the **`product_id`** representing the ProductID of the item being ordered.
- 2 is the **`quantity`** representing the quantity of the product being ordered.

Upon executing this **`CALL`** statement, the **`PlaceOrder`** stored procedure will perform the following tasks:

- Calculate the total price for the specified product and quantity.
- Insert a new record into the **`Orders`** table with the calculated total amount.
- Retrieve the OrderID of the newly inserted order.
- Insert a corresponding record into the **`OrderDetails`** table linking the order with the specific product and quantity.
- Update the inventory by reducing the quantity of the ordered product.

#### Example Scenarios
Here are some additional scenarios showcasing the usage of views and stored procedures:

- **Scenario 1**: Retrieve Order Details for a Specific Customer
```sql
-- Retrieve order details for CustomerID 2 using the view
SELECT * FROM OrderProductDetails WHERE CustomerID = 2;
```
- **Scenario 2**: Place an Order Using the Stored Procedure
```sql
-- Example: Place an order for CustomerID 4 with ProductID 5 and Quantity 3
CALL PlaceOrder(4, 5, 3);
```
- **Scenario 3**: Calculate Total Price Using a Stored Procedure
```sql
-- Calculate the total price for ProductID 10 with Quantity 1
CALL CalculateTotalPrice(10, 1, @total_price);
SELECT @total_price AS TotalPrice;
```
## Conclusion
This guide provides a comprehensive overview of using the **Inventory and Streamline Order Processing database system**. By following the outlined steps, you can effectively set up the 
database schema, insert data, execute queries, and utilize advanced database features like views, functions, and stored procedures to streamline operations and enhance efficiency in
an e-commerce environment. Customize and extend these examples based on your specific business requirements and application needs.
