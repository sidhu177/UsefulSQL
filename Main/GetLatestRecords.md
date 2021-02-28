Supposing you need the lastest records from a table use the MAX() function to get the latest date and filter for that date 

```
SELECT * 
FROM   Table1
WHERE  DateVal in (
                    SELECT MAX(DateVal) 
                    FROM   Table1 
                    )
```

