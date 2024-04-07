# Implementation Details
This document outlines the detailed implementation of a database system designed for an e-commerce platform focused on inventory management and order processing. Below are the specific 
aspects covered:

## Technologies Used
Database: MySQL
SQL for schema creation, data manipulation, views, functions, and stored procedures

## Schema Creation
The schema consists of the following tables:

-Products: Contains information about products available in the inventory.
-Inventory: Tracks the quantity of each product available in stock.
-Customers: Stores customer details for orders.
-Orders: Manages order information, including customer details, order date, total amount, and status.
-OrderDetails: Captures details of each product included in an order.

## Tables Created
- Products:
    - ProductID (Primary Key)
    - ProductName (VARCHAR)
    - Description (TEXT)
    - Price (DECIMAL)
- Inventory:
    - ProductID (Foreign Key referencing Products)
    - Quantity (INT)
- Customers:
    - CustomerID (Primary Key)
    - FirstName (VARCHAR)
    - LastName (VARCHAR)
    - Email (VARCHAR)

- Orders:
    - OrderID (Primary Key)
    - CustomerID (Foreign Key referencing Customers)
    - OrderDate (DATETIME)
    - TotalAmount (DECIMAL)
    - Status (VARCHAR)

- OrderDetails:
    - OrderDetailID (Primary Key)
    - OrderID (Foreign Key referencing Orders)
    - ProductID (Foreign Key referencing Products)
    - Quantity (INT)
    - Price (DECIMAL)
    - Foreign Key Relationships
    - Inventory.ProductID references Products.ProductID
    - Orders.CustomerID references Customers.CustomerID
    - OrderDetails.OrderID references Orders.OrderID
    - OrderDetails.ProductID references Products.ProductID

## Data Insertion
Data was inserted into the database using INSERT INTO statements for Products, Customers, Inventory, Orders, and OrderDetails tables.

## Views, Functions, and Stored Procedures
Views:
- **`OrderProductDetails`**: Retrieves order details along with associated product information.

Stored Procedures:
- **`CalculateTotalPrice`**: Calculates the total price for a given product quantity.
- **`InsertIntoOrders`**: Inserts a new order into the Orders table and retrieves the new order ID.
- **`InsertIntoOrderDetails`**: Inserts order details into the OrderDetails table.
- **`UpdateInventory`**: Updates the inventory quantity after an order is placed.
- **`PlaceOrder`**: Combines the above procedures to place an order for a customer.

## Usage Examples
- Retrieval of orders for a specific customer: **`SELECT * FROM Orders WHERE CustomerID = 3;`**
- Calculation of total sales for a specific product: **`SELECT ProductID, SUM(Quantity) AS TotalQuantity, SUM(Price * Quantity) AS TotalSales FROM OrderDetails GROUP BY ProductID;`**
- Update order status: **`UPDATE Orders SET Status = 'Shipped' WHERE OrderID = 1;`**
- Retrieval of product information with current inventory levels:
```sql
SELECT p.ProductID, p.ProductName, p.Description, p.Price, i.Quantity
FROM Products p
INNER JOIN Inventory i ON p.ProductID = i.ProductID;
```
## Conclusion
In conclusion, this database implementation provides a robust foundation for an e-commerce platform's inventory management and order processing functionalities. The schema design
ensures efficient data storage, retrieval, and manipulation while maintaining data integrity through foreign key relationships. The utilization of views, functions, and stored procedures
enhances query performance and simplifies complex operations, contributing to overall system efficiency and scalability. Further optimization and customization can be applied based on
specific business requirements and performance considerations.
