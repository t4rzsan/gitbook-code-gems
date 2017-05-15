# Coding Standards: T-SQL

## Naming

Use camel notation and capitalize the first letter for tables, views, parameters, and column names.  Do not pluralize names for tables and views.  

```t-sql
CREATE TABLE [Customer]
(
    CustomerID INT NOT NULL,
    Name NVARCHAR(20) NOT NULL
)
```

Postfix id columns with "ID", e.g. CustomerID.



