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
The interesting part of Create Table Expressions is that you can combine multiple queries into a single grand query

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
LEFT JOIN Marketing M 
ON S.SalesTerritory = M.SalesTerritory
AND S.DateColumn = M.DateColumn
```

Notice that Sales and Marketing are two smaller queries that are joined on the Date and SalesTerritory columns to generate the combined view.
