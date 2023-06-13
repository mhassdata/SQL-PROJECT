Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:
SELECT totaltransactionrevenue, city, country
FROM all_sessions
WHERE totaltransactionrevenue IS NOT NULL
GROUP BY city, country, totaltransactionrevenue
ORDER BY totaltransactionrevenue DESC
LIMIT 10


Answer:




**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries: 
SELECT all_sessions.city, all_sessions.country, AVG(products.orderedquantity) AS average_products_ordered
FROM all_sessions
JOIN products ON all_sessions.productsku = products.sku
GROUP BY all_sessions.city, all_sessions.country



Answer:





**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:



Answer:





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:



Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:



Answer:







