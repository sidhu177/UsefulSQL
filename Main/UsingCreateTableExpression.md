Supposing you have columns that need to be grouped and apply manipulations, use create table expression to get the base columns and apply manipulations on the exterior SELECT 

```
WITH CTE AS ( 
     SELECT Text1
        ,   DateColumn
        ,   SUM(Measure1) as Measure1
        ,   SUM(Measure2) as Measure2
    FROM Table1
    GROUP BY Text1, DateColumn
)
SELECT Text1
    ,  DateColumn
    ,  Measure1
    ,  Measure2
FROM CTE 
ORDER BY DateColumn
```
The interesting part of Create Table Expressions is that you can combine multiple queries into a single grand query.

What you can do with Create Table Expressions can also be done using sub queries. CTEs have two advantages , first is that you can have multiple smaller CTEs from various tables and join them to create an extended table. Second is that you can try recursive queries. Here is an example of the first type.

```
WITH Sales as ( 
SELECT SalesTerritory
    ,  DateColumn
    ,  SUM(Sold) as TotalSold
    ,  SUM(Price) as Price 
FROM Sales 
GROUP BY SalesTerritory, DateColumn
),
Marketing as (
SELECT SalesTerritory
    ,  DateColumn
    ,  SUM(Cost) as CampaignCost
FROM Marketing
GROUP BY SalesTerritory, CampaignCost
)
SELECT S.SalesTerritory
    ,  S.DateColumn
    ,  S.TotalSold
    ,  S.Price
    ,  M.CampaignCost
    ,  ((S.TotalSold*S.Price) - M.CampaignCost) as Expense
FROM Sales S 
INNER JOIN Marketing M 
ON S.SalesTerritory = M.SalesTerritory
AND S.DateColumn = M.DateColumn
```

Notice that Sales and Marketing are two smaller queries that are joined on the Date and SalesTerritory columns to generate the combined result.

```
WITH Sales as ( 
SELECT SalesTerritory
    ,  DateColumn
    ,  SUM(Sold) as TotalSold
    ,  SUM(Price) as Price 
    ,  SUM(CASE WHEN SalesTerritory = X THEN Sold*price*0.8
            WHEN SalesTerritory = Y THEN Sold*price*0.75
            ELSE Sold*price
       END) as Discount
FROM Sales 
GROUP BY SalesTerritory, DateColumn
),
Marketing as (
SELECT SalesTerritory
    ,  DateColumn
    ,  SUM(Cost) as CampaignCost
FROM Marketing
GROUP BY SalesTerritory, CampaignCost
)
SELECT S.SalesTerritory
    ,  S.DateColumn
    ,  S.TotalSold
    ,  S.Price
    ,  S.Discount
    ,  M.CampaignCost
    ,  ((S.TotalSold*S.Price) - M.CampaignCost) as Expense
FROM Sales S 
INNER JOIN Marketing M 
ON S.SalesTerritory = M.SalesTerritory
AND S.DateColumn = M.DateColumn
```
The above query demonstrates a useful pattern. You can sum on a case statement. 

Supposing you want to create a running Total for bunch of Salesman. You can use CTE for running Total views that contain all Salesman. Following query will get the Month to Date and will show 0 for Salesman that have no records for the date instead of not displaying the salesman.

```
WITH Salesman as ( 
SELECT DISTINCT Salesman
    ,  DateColumn
FROM Sales 
),
Sales as (
SELECT Salesman
    ,  DateColumn
    ,  Sales
FROM Sales
GROUP BY Salesman, CampaignCost
)
SELECT a.Salesman
    ,  a.DateColumn
    ,  b.Sales
    ,  SUM(b.Sales) OVER(PARTITION BY a.Salesman, DATE_FORMAT(a.DateColumn,'%Y-%m') ORDER BY a.DateColumn DESC ) MTD
FROM Salesman a 
LEFT JOIN Sales b 
ON S.SalesTerritory = M.SalesTerritory
AND S.DateColumn = M.DateColumn
```
