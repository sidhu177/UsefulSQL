Supposing you need the lastest records from a table use the MAX() function to get the latest date and filter for that date . 

```
SELECT * 
FROM   Table1
WHERE  DateVal in (
                    SELECT MAX(DateVal) 
                    FROM   Table1 
                    )
```

Supposing you need the latest record per month , then you would need to do a group by month and year to get the single latest record per month 

```
SELECT * 
FROM   Table1
WHERE  DateVal in (
                    SELECT MAX(DateVal) 
                    FROM   Table1
                    GROUP BY MONTH(DateVal), YEAR(DateVal) 
                    )
```

Above query can also be written as 

```
SELECT * 
FROM   Table1
WHERE  DateVal in (
                    SELECT MAX(DateVal) 
                    FROM   Table1
                    GROUP BY Date_Format(DateVal,'%Y-%m') 
                    )
```

```
SELECT * 
FROM   Table1
WHERE  DateVal in (
                    SELECT MAX(DateVal) 
                    FROM   Table1
                    GROUP BY CONCAT(Year(DateVal),-,Month(DateVal)) 
                    )
```
