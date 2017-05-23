# 

# 

# Coding Standards: T-SQL

## Naming

Some guidelines for writing T-SQL in random order.

Use camel notation and capitalize the first letter for tables, views, parameters, and column names.  Do not pluralize names for tables and views.

```sql
CREATE TABLE Customer
(
    CustomerID INT NOT NULL,
    Name NVARCHAR(20) NOT NULL
)
```

Postfix id columns with "ID", e.g. CustomerID.

Never use underscores in names.

## Defining constraints

Create keys and contraints as named constraints.

```sql
CREATE TABLE Customer
(
    CustomerID INT NOT NULL,
    Name NVARCHAR(20) NOT NULL,
    CONSTRAINT PK_Customer_CustomerID PRIMARY KEY CLUSTERED (CustomerID)
)

CREATE TABLE Order
(
    OrderID INT NOT NULL,
    CustomerID INT NOT NULL,
    CONSTRAINT PK_Order_OrderID PRIMARY KEY CLUSTERED (OrderID)
)

ALTER TABLE 
ADD CONSTRAINT FK_Order_Customer FOREIGN KEY (CustomerID)     
REFERENCES Customer (CustomerID)
```

## NULL

Try to avoid columns that allow NULL.

Never compare a value to NULL using "=", "&lt;&gt;", nor "IN".  This may lead to unpredictable results.  Always use IS NULL or NOT IS NULL.

## Commas

In column lists, start a new line with a comma.

```sql
SELECT
CustomerID
, Name
FROM Customer
```

## Indentation

There are many ways to layout your SQL. Please use whatever layout you prefer, must be consistent.  I usually left-align all kewords but indent nested SQL, such as CTEs and CASE statements.  But I always do it the same way.

```sql
SELECT
Customer.CustomerID
, Customer.Name
FROM Customer
JOIN Order
ON Customer.CustomerID = Order.CustomerID
```

## Casing

Either use all-caps or non-caps for keywords.  Never mix them.

```sql
-- Do
SELECT
Customer.CustomerID
, Customer.Name
FROM Customer
JOIN Order
ON Customer.CustomerID = Order.CustomerID

-- Do
select
Customer.CustomerID
, Customer.Name
from Customer
join Order
on Customer.CustomerID = Order.CustomerID

-- Don't
Select
Customer.CustomerID
, Customer.Name
From Customer
Join Order
on Customer.CustomerID = Order.CustomerID
```

## Aliases
Try to use meaningful aliases for tables and not too many meaningless abbrevations. 
Prefix your column names if there can be any doubt as to what table or view the column
comes from.

```sql
-- Do
SELECT
Customer.CustomerID
, Customer.Name
FROM Customer
JOIN Order
ON Customer.CustomerID = Order.CustomerID

-- Don't
SELECT
CustomerID
, Name
FROM Customer
JOIN Order
ON Customer.CustomerID = Order.CustomerID

```

