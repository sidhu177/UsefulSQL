Some SQL databases like postgres and SQL Server allow Set operations like Except and Intercept. MySQL does not. 

Using Except can make it easy to find values that exist in one table but do not exist in the other tables. 

```
SELECT Col1 
FROM Table1 
EXCEPT 
SELECT Col2 
FROM Table2
```
Now Col1 of Table1 should be the same entity attribute as in Col2 of Table2 then that will return only those values that are in Table1 but not in Table2

To get the values that exist in both tables use INTERSECT

```
SELECT Col1 
FROM Table1 
INTERSECT 
SELECT Col2 
FROM Table2
```

To get all the values in both tables use UNION

```
SELECT Col1 
FROM Table1 
UNION
SELECT Col2 
FROM Table2
```