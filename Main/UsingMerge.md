Supposing you want to get data from a source table to a target table, you can achieve that with a MERGE 

MERGE INTO Table1 USING Table2 ON Table1.dimension1 = Table2.dimension1
 WHEN MATCHED THEN UPDATE SET measure1 = measure1 + Table2.measure1
 WHEN NOT MATCHED THEN INSERT VALUES (Table2.dimension1, Table2.measure1);


MERGE is one of the powerful SQL Keywords I've had to work with and plays important role when building Data flows using stored procedures.