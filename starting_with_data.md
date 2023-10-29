Question 1: unique and distinct fullvisitorid in all_sessions table

SQL Queries:select distinct (fullvisitorid)
from all_sessions

Answer: 14223 records



Question 2: find all duplicate data in fullvisitorid column in all_sessions table

SQL Queries:

SELECT fullvisitorid, COUNT(*) as duplicate_count_number
FROM all_sessions
GROUP BY fullvisitorid
HAVING COUNT(*) > 1;

Answer: 794 records



Question 3: changing date varchar string into date timestamp datatype in pgadmin

SQL Queries:
SELECT 
distinct s.date::date AS date_column
FROM all_sessions s;

Answer: 366 records



Question 4: which city user is spending more time on site ?

SQL Queries:
select city,
SUM(timeonsite) AS totalsum_time_spent
FROM
   All_sessions

where 	
city is Not Null 
And
timeonsite is not null 


GROUP BY city
ORDER BY totalsum_time_spent DESC   --(highest to lowest)
 
 --LIMIT 1; if we are looking t o the highest one 

Answer: 248 records



Question 5: find each unique product viewed by each visitor

SQL Queries: 
SELECT
    Distinct fullvisitorid,
    v2productname
FROM
    all_sessions

WHERE
    fullvisitorid IS NOT NULL
    AND v2productname IS NOT NULL

GROUP BY
    fullvisitorid, v2productname;  -- unique visitor for each product


Answer:15115 records
