Say you want to get the Year to Date on total Sales or expenses, using a OVER(PARITION BY ...) makes like so much more easy.

```
SELECT Salesman
    ,  DateColumn
    ,  SUM(Sales) OVER (PARITION BY Salesman, YEAR(DateColumn) ORDER BY DateColumn DESC) as YTD
FROM Sales a
```