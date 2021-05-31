SQL code also needs to have good formatting. Just like you have formatting rules styling guides for python, java and the likes, formatting SQL code is as important if not more. Consider the following paragrpah style

```
SELECT Dim1, Dim2, CAST(Datevalue as DATE) DateVal, SUM(Measure1), SUM(Measure1) OVER(PATITION BY Dim1) Total, COUNT(DISTINCT Dim1) cnt FROM TABLE1 WHERE CAST(DateValue as DATE) >= '2021-01-01' GROUP BY Dim1 ORDER BY CAST(DateValue as DATE) DESC
```

For those who made the query it might make sense but a new set of eyes is going to take some time to be able to make sense of it, Instead consider the following format. 

```
SELECT Dim1
    ,  Dim2
    ,  CAST(Datevalue as DATE) DateVal
    ,  SUM(Measure1) Agg
    ,  SUM(Measure1) OVER(PATITION BY Dim1) Total
    ,  COUNT(DISTINCT Dim1) cnt 
FROM TABLE1 
WHERE CAST(DateValue as DATE) >= '2021-01-01' 
GROUP BY Dim1 
ORDER BY CAST(DateValue as DATE) DESC
```

By Virtue of calling out each column on a separate line it makes the query look uncluttered and easy to read And if there is any aggregation on a column like a SUM() or a COUNT() that would be clearly distinguishable as opposed to the paragraph style wherein it becomes confusing really quick.

Calling out the JOIN types explicitly helps the reader comprehend the relationship between tables. Implicit join conditions make the WHERE condition cluttered and the join type is not clear to the reader.

```
SELECT ....
FROM TABLE1 t1, TABLE2 t2, Table3 t3 
WHERE t1.Dim1 = t2.Dim1 
AND t1.DateValue = t3.DateValue
AND CAST(DateValue as DATE) >= '2021-01-01'
```

Instead consider the following

```
SELECT .....
FROM TABLE1 t1 
INNER JOIN TABLE2 t2
on t1.Dim1 = t2.Dim1 
LEFT JOIN Table3 t3
on t1.DateValue = t3.DateValue 
WHERE CAST(DateValue as DATE) >= '2021-01-01' 
GROUP BY Dim1 
ORDER BY CAST(DateValue as DATE) DESC
```

Now I get that formatting is largely an individual preference but when working in Production environments its higly likely that a script set in production will have to be read by another Developer either for troubleshooting or development. As such having formatting standards like PEP8 in python will help in making SQL code maintenance.
