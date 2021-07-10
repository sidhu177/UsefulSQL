Joins are a fundamental SQL operation. They allow you to combine more than one table and return result. Joins are the main reason for success of relational databases popularity.

Joins happen at row level. so every time table A joins with table B on ID its going to return a record. 

Consider the following :
        Table1 has only a primary key (accountID) 
        Table2 has that as a foriegn key (accountID)
        Table1 has only one record per accountID
        Table2 has multiple record per accountID

        Table1 LEFT JOIN Table2 will return as many records proportionate to the accountIDs in Table2 even if its a LEFT JOIN with Table1 which has only one acocuntID per record.    
