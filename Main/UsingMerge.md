Supposing you want to get data from a source table to a target table, you can achieve that with a MERGE 

```
MERGE INTO Table1 
USING Table2 
ON Table1.Hash = Table2.Hash
WHEN MATCHED THEN 
UPDATE SET measure1 = measure1 + Table2.measure1
WHEN NOT MATCHED THEN 
INSERT VALUES (Table2.dimension1, Table2.measure1);
```

MERGE is one of the powerful SQL Keywords I've had to work with and plays important role when building Data flows using stored procedures.

An example workflow is getting a csv file into a landing table and then merging with Staging table which inturn gets merged into Dimension and later Reporting table/view

.csv --> Lnd --> Stg --> Dim --> Rpt  

where Landing table is a truncate and load table containing only current day's data and Staging table contains historical data.

Dimension tables are usually a collection of Name, Date and Qualitative fields from different sources Whereas Fact tables are quantitative fields from different sources. The idea behind making dimension and fact tables are to make it easy for reporting to get the Data for visualization. Usual star schema has one Dimension table with multiple fact tables. So one customer's information is divided into many tables when storing and re-aggregated when reporting.

Merging from Landing to Staging is usually done on Hash comparison

```
/* Temporary table for merge results */

     CREATE TABLE #ResultCount
     (Action VARCHAR(20));
   
	 /* Merge */

with table1 as 
(select Col1
      , Col2
      , Col3
	  , LOADDATE
      , LOADID
	  from sch.lnd_table1 )
	  
	  MERGE sch.table2 STG
	  USING ( select table1.*,
	  CONVERT( VARCHAR(50)
            ,  HASHBYTES('MD5', CONCAT(CONVERT(VARCHAR, Col1)
                              , convert(varchar,Col2)
                              , convert(varchar,Col3))),2) as lnd_hash 
	  from table1) as LND
	 
	  on LND.Col1 = STG.Col1
	 
	  WHEN MATCHED 
AND (LND.Col2 <> STG.Col2) OR (LND.LND_HASH != STG.STG_HASH)

THEN 
UPDATE
SET Col1 = lnd.Col1
,Col2 = lnd.Col2
,Col3 = lnd.Col3
,[LOADDATE] = lnd.[LOADDATE]
,[LOADID] = lnd.[LOADID]
,[STG_HASH] =lnd.[LND_HASH]
,[UpdateType] = 'U'
,[UpdateDate] = GETDATE()

WHEN NOT MATCHED THEN 
INSERT(Col1
,Col2
,Col3
,[LOADDATE] 
,[LOADID] 
,[STG_HASH] 
,[UpdateType] 
,[UpdateDate] 

VALUES(
lnd.Col1
,lnd.Col2
,lnd.Col3
,[LOADDATE]
,lnd.[LOADID]
,lnd.[LND_HASH]
,'I'
, GETDATE())
	  
	  OUTPUT $ACTION
                 INTO #ResultCount(Action);

	 /* Output merge results */

     SELECT @inserted = COUNT(*)
     FROM #ResultCount
     WHERE Action = 'INSERT';
     SELECT @updated = COUNT(*)
     FROM #ResultCount
     WHERE Action = 'UPDATE';

```

its useful to have a resultcount Temporary table that will store the insert and update counts for historical records