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