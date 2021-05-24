Stored procedures are an interesting encapsulation of SQL logic. It allows for orchestration of tasks that can be compiled into a single file and get executed at scheduled times. For example, loading a table at 1 am every day. To use a real world scenario, you would need to load a table at 1 am everyday with latest data. The Source and the Target tables dont change. The timining is fixed. The easiest way to achieve this is to encapsulate the logic in a stored procedure. Like 

```
CREATE PROCEDURE public.Load_Marketing_Table AS 

TRUNCATE TABLE public.lnd_marketing 

SELECT * FROM source.marketing INTO public.lnd_marketing

```

Above is a very simplified example of taking data from source.marketing and loading on to public.lnd_marketing. Established Data Warehouses have such type data flows from landing tables all the way to staging -> dimension -> fact -> reporting tables. Most of the data flow is orchestrated using stored procedures.