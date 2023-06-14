Question 1: What is the average time on site in minutes for purchased products by country?

SQL Queries:

TOP 5 COUNTRIES HIGHEST AVG TIME SPENT BY COUNTRY

SELECT cl.country, CAST (AVG(time_on_site/60) AS DECIMAL(10,2)) AS avg_time_onsite
FROM cleaned_analytics AS a 
JOIN cleaned_sessions AS cl 
ON a.visitid = cl.visit_id 
WHERE a.units_sold IS NOT NULL 
GROUP BY cl.country 
ORDER BY avg_time_onsite DESC

THE LOWEST 5 AVG TIME SPENT BY COUNTRY

SELECT cl.country, CAST (AVG(time_on_site/60) AS DECIMAL(10,2)) AS avg_time_onsite
FROM cleaned_analytics AS a 
JOIN cleaned_sessions AS cl 
ON a.visitid = cl.visit_id 
WHERE a.units_sold IS NOT NULL 
GROUP BY cl.country 
ORDER BY avg_time_onsite ASC

Answer: 

TOP 5 COUNTRIES HIGHEST AVERAGE TIME 

1-THAILAND 33 MINUTES
2- TAIWAN 23.50 MINUTES
3- EGYPT 23 MINUTES
4- SINGAPORE 22 MINUTES
5- NETHERLANDS 19.60

LOWEST 5 AVG TIME SPENT BY COUNTRY

1-DENMARK 0.00 MINUTES
2-MEXICO 0.50 MINUTES
3- IRELAND 1 MINUTE
4 ROMANIA 2 MINUTES
5-COLUMBIA 2 MINUTES

Based on these findings there is a range of 0-33 minutes of average time when categorized by country.




Question 2: Is there a relationship between Sentiment sscore and the Highest revenue products sold?

SQL Queries:

CREATE TEMPORARY TABLE TO JOIN TABLES PRODUCTS AND CLEANED_SESSIONS

CREATE TEMPORARY TABLE products_sessions AS (
SELECT *
FROM cleaned_sessions AS cl
JOIN products AS p 
ON p.sku = cl.product_sku)


SELECT p.v2product_name, p.sentimentscore, SUM(a.units_sold * p.product_price) AS total_revenue
FROM cleaned_analytics AS a 
JOIN products_sessions AS p
ON a.visitid = p.visit_id 
WHERE a.units_sold IS NOT NULL 
GROUP BY p.v2product_name, p.sentimentscore 
ORDER BY total_revenue DESC 
Answer:

Top 3 highest products sold and their magnitude score.

1-Google ALpine Style Backpack, 0.6 , $22697.73
2- Nest Learning Thermostat 3rd Gen USA White, 0.3, $4732.00
3- Nest Learning Thermostat 3rd Gen USA Stainless Steele 0.3, $ 4421.00

Question 3: Is there a relationship with most sold products and value of customer to company?

SQL Queries:
Top 3 Highest Magnitude Score

USING THE TABLE CREATED IN QUESTION 4 WE USED THIS QUERY

TOP 3 PRODUCTS WITH THE HIGHEST MAGNITUDE SCORE 

SELECT p.sentimentmagnitude, p.v2product_name, p.product_price, SUM(a.units_sold) AS total_units
FROM cleaned_analytics AS a 
JOIN products_sessions AS p
ON a.visitid = p.visit_id 
WHERE a.units_sold IS NOT NULL 
GROUP BY p.sentimentmagnitude, p.v2product_name, p.product_price
ORDER BY p.sentimentmagnitude DESC
LIMIT 3

TOP 3 MOST PRODUCTS SOLD 

SELECT p.sentimentmagnitude, p.v2product_name, SUM(a.units_sold * p.product_price) AS total_revenue
FROM cleaned_analytics AS a 
JOIN products_sessions AS p
ON a.visitid = p.visit_id 
WHERE a.units_sold IS NOT NULL 
GROUP BY p.sentimentmagnitude, p.v2product_name 
ORDER BY total_revenue DESC
LIMIT 3


Answer:
TOP 3 HIGHEST MAGNITUDE SCORES 

1-Google Mens Quilted Insulated Vest Black, 1 unit sold, $74.00, 2
2- Android Mens Long Sleeve Badge Crew Tee Heather 8 Units sold, $34.99, 8, 1.8 
3- Youtube Mens Vintage Tank 6 Units Sold, 1.8

Top 3 Most Sold products 

1- Google Alpine Style Backpack , 227 Units sold, $22,697.75, 0.9
2- SPF-15 Slim & slender Lip Balm, 168 Units sold, $3849.45, 1.5
3- Google Mens Airflow 1/4 Zip Pullover Black, 1 units sold, $2980.00, 0.5

Though there products with the highest magnitude score have low amount of sold products when looking at the most sold products list 2 out of the top 3 products have a high magnitude score therefore there is a relationship with high sales and a customers purchasing value to a company.

Question 4: 

SQL Queries:

Answer:



Question 5: 

SQL Queries:

Answer:
