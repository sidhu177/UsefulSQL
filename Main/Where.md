Filtering in relational databases is done using Where condition. A less known fact is that WHERE is the first syntax that gets executed in SQL, Its a powerful syntax and should be used with caution.

```
SELECT *
FROM   Table1
WHERE dim1 = 'A'
AND   dim2 < '2021-06-05'
AND   (dim3 = 'B' OR dim4 = 0 OR dim5 = 'C' )
```

