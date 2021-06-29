Filtering in relational databases is done using Where condition. A less known fact is that WHERE is the first syntax that gets executed in SQL, Its a powerful syntax and should be used with caution.

```
SELECT *
FROM   Table1
WHERE dim1 = 'A'
AND   dim2 < '2021-06-05'
AND   (dim3 = 'B' OR dim4 = 0 OR dim5 = 'C' )
```

Here is another example from HackerRank SQL exercise. Get cities that start and end with a,e,i,o,u

```
SELECT DISTINCT CITY
FROM STATION
WHERE substring(CITY,1,1) in ('a','e','i','o','u') 
AND (lcase(CITY) like '%a'
OR lcase(CITY) like '%e'
OR lcase(CITY) like '%i'
OR lcase(CITY) like '%o'
OR lcase(CITY) like '%u')
```

WHERE clause is the first syntax that is executed when compiling a SQL Query.

```
SELECT col1
    ,  Col2
FROM   Table1
WHERE  col1 = 'A'
```

Above query first executes the WHERE clause and sets the filter to get rows where Col1 is A and then projects Col1 and Col2. The sequence of filters in WHERE also matters

```
SELECT col1
    ,  Col2
FROM   Table1
WHERE  partition_column = 'A'
        AND col2 = 'B'
```
has the effect of getting all the 'A' in the partition_column and then filtering for 'B' Note that this is not the same as getting 'B' first and then applying partition_column