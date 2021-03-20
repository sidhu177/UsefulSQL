Supposing you want to find Duplicates in a Table, you can do the following query

```
SELECT Dimension
    ,  count(*)
FROM Table
GROUP BY Dimension 
HAVING count(*)>1
```

Where Dimension is a string column like City or Salesman 