One useful feature of SQL that doesnt get a lot of attention is DynamicSQL. This allows for storing constants that can be used in the query. Like for example.

```
DECLARE @PrevDate DATE

SET @PrevDate = '2021-05-31'

SELECT *
FROM   Table1
WHERE  Loaddate = @PrevDate
```
Above is a SQL Server specific example but you get the point. Declaring variable types and storing values come in super handy when working on Stored Procedures and functions. 



