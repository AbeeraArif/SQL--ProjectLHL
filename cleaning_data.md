What issues will you address by cleaning the data?
Issues i will adress to clean data in project Database:
to have checked Null values /empty fields not to use for calculations
to have correct datatypes for columns I am going to use in my project
to have PK and FK not as empty fields or NUll values
data should be in consistent format

Queries:
Below, provide the SQL queries you used to clean your data.
e.g: SELECT
    city AS City,
    country AS Country,
    SUM(totaltransactionrevenue)AS Total_Revenue
FROM
    all_sessions
	  where   city IS NOT NULL  -- filtering out NUll values 
    AND country IS NOT NULL
    AND totaltransactionrevenue IS NOT NULL
GROUP BY
    city, country
ORDER BY
    Total_Revenue Desc;
