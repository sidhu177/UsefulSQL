Say you want to get the Year to Date on total Sales or expenses, using a OVER(PARITION BY ...) makes like so much more easy.

```
SELECT Salesman
    ,  DateColumn
    ,  SUM(Sales) OVER (PARITION BY Salesman, YEAR(DateColumn) ORDER BY DateColumn DESC) as YTD
FROM Sales a
```

OVER (PARITION BY ...) syntax is really powerfull in getting aggregations and Rank per Dimension. You want to know comparative performance of Salesman per year you can use Rank OVER() , you want to know month to date sales, for that too you can use OVER (Partition by)

```
SELECT Salesman
    ,  DateColumn
    ,  SUM(Sales) OVER (PARITION BY Salesman, DATE_FORMAT(DateColumn,'%Y-%m') ORDER BY DateColumn DESC) as MTD
    ,  SUM(Sales) OVER (PARITION BY Salesman, YEAR(DateColumn) ORDER BY DateColumn DESC) as YTD
FROM Sales a
```