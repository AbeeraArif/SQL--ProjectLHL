Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:


SELECT
    city AS City,
    country AS Country,
    SUM(totaltransactionrevenue)AS Total_Revenue
FROM
    all_sessions
    
	where   city IS NOT NULL
    AND country IS NOT NULL
    AND totaltransactionrevenue IS NOT NULL
    
GROUP BY
    city, country
ORDER BY
    Total_Revenue Desc;


Answer:21 records showing totalrevenue grouped by city totheir respective country 




**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:


SELECT
    alls.city AS City,
    alls.country AS Country,
    AVG(po.orderedquantity) AS Average_Products_Ordered
    
    FROM     all_sessions AS alls
    JOIN     products AS po ON alls.productsku = po.sku
	
 
 where 
    orderedquantity is not null
	and alls.city is not null
	and alls.country is not null


group by
    alls.city, alls.country

ORDER BY
    Average_Products_Ordered DESC; -- avg number of products ordered in city n country from highest to lowest



Answer: 428 records





**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries: -- using 2 CTE

WITH ProductCounts AS (
    SELECT
        city AS City,
        country AS Country,
        V2productcategory AS Product_Category,
        COUNT(*) AS Product_Count
    
    FROM
        allsessionsclean3
    GROUP BY
        city, country, product_category
),

RankedProducts AS (
    SELECT
        City,
        Country,
        Product_Category,
        Product_Count,
        RANK() OVER ( partition by city,country  ORDER BY Product_count DESC) AS Ranknumber
    
    FROM
        ProductCounts
)
-- now selecting product count and rank number as well from CTE and using valid data only 
SELECT
    City,
    Country,
    Product_Category,
    Product_Count,
    Ranknumber
FROM
    RankedProducts
	where city <> '(not set)' and country <> '(not set)'
ORDER BY
    City, Country, Ranknumber;
	



Answer: 1877 records
US orders men -tshirts more - checking at highest order number and 1st rank - we can check the pattern of which product is more ordered in country and city 





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:

WITH RankedProducts AS 

(
    SELECT
        country,
        v2productname,
	-- count all products , row number gives unique number to each country and 
    -- respective count of products in desc ordering (high to low) call it rank-
        
        COUNT(*) AS countofproducts,
        row_number() OVER (PARTITION BY country 
						ORDER BY COUNT(*) desc) AS rankorder 

    
FROM         allsessionsclean4
    
GROUP BY
        country,v2productname
)

SELECT
    country,
  v2productname,
    countofproducts,
	rankorder
FROM
    RankedProducts
WHERE
    country <> '(not set)'
    rankorder = 1  -- filtering first position only
ORDER BY
    country;

Answer: 82 records
showing country thiers highest selling product count and their 1st rank accordingly -





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:

SELECT
    city , -- grouping by city only 
    SUM(transactionrevenue) AS total_revenue
FROM
    all_sessions

where transactionrevenue >1 and transactionrevenue is not null and
city <> 'not available in demo dataset'

GROUP BY
    city

Answer: tried only to find out the city and respective country with most revenue collected
1 answer







