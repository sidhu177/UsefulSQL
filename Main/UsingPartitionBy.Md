Supposing you want to get aggregation with respect to a dimension Parition BY can act wonders to get desired aggregation

```
SELECT Dimension1
    ,  DateValue
    ,  SUM(Measure) OVER(PARTITION BY Dimension1 ORDER BY DateValue DESC) AggPerDim1
FROM Table
ORDER BY DateValue DESC
```

Supposing you want to know relative position of one Dimension with respect to the group, like find the standing of a Salesman in the group. You can use Rank OVER(Partition By..)

```
SELECT Dimension1
    ,  DateValue
    ,  Rank OVER(PARTITION BY Dimension1 ORDER BY DateValue DESC) rk
FROM Table
ORDER BY DateValue DESC
```

Another important window function is the Row_Number() 

```
SELECT Dimension1
    ,  DateValue
    ,  Row_Number() OVER(PARTITION BY Dimension1 ORDER BY DateValue DESC) rn
FROM Table
ORDER BY DateValue DESC
```

This gives a row number based on the columns that the window is partitioned by.

DENSE_RANK is another useful function 

```
SELECT Dimension1
    ,  DateValue
    ,  DENSE_Rank OVER(PARTITION BY Dimension1 ORDER BY DateValue DESC) rk
FROM Table
ORDER BY DateValue DESC
```
