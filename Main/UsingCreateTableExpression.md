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