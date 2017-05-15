# Coding Standards: T-SQL

Some guidelines for writing T-SQL in random order.

Use camel notation and capitalize the first letter for tables, views, parameters, and column names.  Do not pluralize names for tables and views.

```sql
CREATE TABLE [Customer]
(
    CustomerID INT NOT NULL,
    Name NVARCHAR(20) NOT NULL
)
```

Postfix id columns with "ID", e.g. CustomerID.

Create keys and contraints as named constraints.

```sql
CREATE TABLE [Customer]
(
    CustomerID INT NOT NULL,
    Name NVARCHAR(20) NOT NULL,
    CONSTRAINT PK_Customer_CustomerID PRIMARY KEY CLUSTERED (CustomerID)
)
```





