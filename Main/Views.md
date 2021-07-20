Views are very useful in isolating selected columns into a table type object. The difference between a view and table is that tables are physically stored on a Database, Views get built when they are invoked by a SELECT query. 

```
CREATE View public.Marketing_view AS 

SELECT a.Dim1
    ,  a.Dim2
    ,  b.Dim3
    ,  a.Measure1
    ,  b.Measure2
FROM Table1 a 
JOIN Table2 b 
on a.Dim1=b.Dim3 
```

With the above view defined, we dont have to write the SELECT query every time you want to link Table1 and Table2, you just invoke the view 

```
SELECT * FROM public.Marketing_view
```