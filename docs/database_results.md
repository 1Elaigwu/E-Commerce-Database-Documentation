# Database Operations Summary
## Database Schema
### Tables
- **Products**
    - Contains information about various products available in the inventory.
- **Inventory**
    - Tracks the quantity of each product available in stock.
- **Customers**
    - Stores customer details such as name and email.
- **Orders**
    - Manages customer orders including order date, total amount, and status.
- **OrderDetails**
    - Records specific product details (quantity, price) associated with each order.

## Data Insertion
- **Products**
  - **Inserted Products**:
      - A range of products were added to the database including laptops, smartphones, tablets, and more.
- **Customers**
  - **Inserted Customers**:
      - Five customers were added with their names and email addresses.
- **Inventory**
  - **Initial Inventory**:
      - Quantities were set for each product in the inventory.

## Sample Queries and Updates
### Orders
  - **New Orders**:
        - Several new orders were placed by different customers.

  - **Order Updates**:
        - Order details such as order date, total amount, and status were updated for specific orders.

### OrderDetails
  - **Order Details**:
        - Details of specific products (quantity, price) associated with each order were recorded.

## Data Retrieval
- **Retrieving Products**:
    - All product information including name, description, price, and current quantity in stock.

- **Retrieving Orders by Customer**:
    - Orders placed by specific customers were retrieved based on customer ID.

- **Calculating Total Sales**:
    - Total quantity sold and total sales revenue for each product were calculated.

- **Product Information with Inventory Levels**:
    - Combined information showing product details along with current inventory levels.

## Database Optimizations
### Indexes
- **Created Indexes**:
  - Indexes were added on key columns like **`ProductID`** and **`CustomerID`** for faster data retrieval.

### Views
- **Created View**s:
  - A view **`OrderProductDetails`** was created to simplify querying order details with product information.

### Stored Procedures
- **Stored Procedures**:
    - Procedures like **`PlaceOrder`**, **`CalculateTotalPrice`**, **`InsertIntoOrders`**, and **`UpdateInventory`** were defined to streamline common operations.
