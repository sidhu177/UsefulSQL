SubQueries are often used in production SQLs for getting aggregated data used for reporting dashboards or for loading tables to persist aggregated information. Here is an example of a SubQuery

```
SELECT SalesTerritory
    ,  DateColumn
    ,  SUM(Sold) as TotalSold
    ,  SUM(Price) as Price 
FROM (
SELECT t1.SalesTerritory
    ,  t1.DateColumn
    ,  t1.Sold 
    ,  t2.Price
FROM Table1 t1 
INNER JOIN Table2 t2 
ON t1.SalesTerritory = t2.SalesTerritory
AND t1.DateColumn = t2.DateColumn
) as sub 
GROUP BY SalesTerritory, DateColumn
``` 

In the above example the inner query , also called sub query is more granular with respect to the data it gets from tables. Having another SELECT allows for aggregating data at required levels.

Here is an example of cascaded sub query 

```
SELECT * 
FROM Table1 
WHERE Dim1 in ( 
                SELECT Dim1 FROM Table2 
                WHERE Dim2 in ( 
                                SELECT Dim2 FROM Table3 
                                Where Dim4 = 'A' 
                                )
                )
```

An interesting type of SELECT statement is the following

```
SELECT 
       (SELECT Dim1
       FROM Table1
       WHERE Dim2='A'
       ) as Dim1 
    ,  (SELECT Dim1 
        FROM Table2
        WHERE Dim2='B'
       ) as Dim2 
    ,  Dim1 
FROM Table3    
```
