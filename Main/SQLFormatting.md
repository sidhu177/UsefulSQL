SQL code also needs to have good formatting. Just like you have formatting rules styling guides for python, java and the likes, formatting SQL code is as important if not more. Consider the following

SELECT Dim1, Dim2, CAST(Datevalue as DATE) DateVal, SUM(Measure1), SUM(Measure1) OVER(PATITION BY Dim1) Total, COUNT(DISTINCT Dim1) cnt FROM TABLE1 WHERE CAST(DateValue as DATE) >= '2021-01-01' GROUP BY Dim1 ORDER BY CAST(DateValue as DATE) DESC

For those who made the query it might make sense but a new set of eyes is going to take some time to be able to make sense of it. Instead consider the following format. 

```
SELECT Dim1
    ,  Dim2
    ,  CAST(Datevalue as DATE) DateVal
    ,  SUM(Measure1)
    ,  SUM(Measure1) OVER(PATITION BY Dim1) Total
    ,  COUNT(DISTINCT Dim1) cnt 
FROM TABLE1 
WHERE CAST(DateValue as DATE) >= '2021-01-01' 
GROUP BY Dim1 
ORDER BY CAST(DateValue as DATE) DESC
```

By Virtue of calling out each column on a separate line it makes the query look uncluttered and easy to read.  
