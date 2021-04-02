Supposing you want to do a IF type projection of dimensions on your SELECT statement, you can use CASE statement

```
SELECT Dimension1
    ,  CASE WHEN Dimension1 = A THEN 'Asia'
            WHEN Dimension2 = E THEN 'Europe'
        END Zone
FROM Table 
```

you can also do Cascaded CASE statement 

```
SELECT Dimension1
    ,  CASE WHEN Dimension1 = A THEN 
                                    CASE WHEN Dimension2 = SE THEN 'South East'
                                         WHEN Dimension2 = E THEN 'East'
                                         ELSE 'Middle East'
                                    END   
            WHEN Dimension2 = E THEN 'Europe'
        END Zone
FROM Table 
```