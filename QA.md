What are your risk areas? Identify and describe them.
Data Integrity:

like : 
checking risk as inaccurate Data in records given to us in database - Data in each feild should be correct and complete.
making sure not using duplicate data to aviod data redundancy 
primary keys, foreign keys should be should with valid data types and no null , empty field with unique values.
consistency with decimal values and data type 
back up and recovery should also be considered to have backup tables and using data set from creating new tables from already given raw dataset - making sure not to make any chanes into real raw dataset - infact if we have to update any field - create new normalized table and perform queries on new table.

QA Process:
Describe your QA process and include the SQL queries used to execute it.

1: Using unique and distinct fullvisitorid - not using duplicates if present

select distinct (fullvisitorid)
from all_sessions

2: making sure data type is present as consistent through out with correct data type

SELECT 
    distinct s.date::date AS date_column
FROM all_sessions s;

3: creating new clean tables for new queries , not using null values or feilds with no data 

CREATE TABLE allsessionsclean4 AS
SELECT city,country, v2productname

FROM all_sessions

WHERE
    city IS NOT NULL
    AND country IS NOT NULL
    AND v2productname IS NOT NULL
    AND city <> '(not set)' and city <> 'not available in demo dataset'
    AND country <> '(not set)' and  country <> 'not available in demo dataset'
    AND v2productname <> '(not set)' and  v2productname <> 'not available in demo dataset';
