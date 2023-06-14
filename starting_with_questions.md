Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:
QUERY TO SEE TOP 5 COUNTRIES WITH HIGEST REVENUE ON SITE 

SELECT cl.country, SUM(a.units_sold * cl.product_price) AS total_revenue
FROM cleaned_analytics AS a
JOIN cleaned_sessions AS cl
ON a.visitid = cl.visit_id
WHERE a.units_sold IS NOT NULL
GROUP BY cl.country
ORDER BY total_revenue DESC 
LIMIT 5

QUERY TO SEE TOP 5 CITIES WITH HIGHEST REVENUE ON SITE

SELECT cl.city, SUM(a.units_sold * cl.product_price) AS total_revenue
FROM cleaned_analytics AS a
JOIN cleaned_sessions AS cl
ON a.visitid = cl.visit_id
WHERE a.units_sold IS NOT NULL
GROUP BY cl.city
ORDER BY total_revenue DESC 
LIMIT 5


Answer:

THE TOP 5 CITIES WITH HIGHEST REVENUES:

NEW YORK $17038.73
CHICAGO $8756.63
**NOT AVAILABLE IN DATA SET** $7517.92 (REQUIRES FURTHER INVESTIGATION)
MOUNTAINVIEW $6508.69
SUNNYVALE $1694.13

TOP 5 COUNTRIES WITH HIGHEST REVENUE:

UNITED STATES $46076.81
HONG KONG $ 532.99
MEXICO $ 267.99
MALDIVES $239.98
IRELAND $239.96


**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries: THE TOP 5 PRODCTS ORDERED AVERAGES GROUPED BY COUNTRY

SELECT cl.country, CAST(AVG(a.units_sold) AS decimal(10,2)) AS avg_units_sold
FROM cleaned_analytics AS a
JOIN cleaned_sessions AS cl
ON a.visitid = cl.visit_id
WHERE a.units_sold IS NOT NULL
GROUP BY cl.country
ORDER BY avg_units_sold DESC

TOP 5 PRODUCTS ORDERED AVERAGES GROUPED BY CITIES

SELECT cl.city, CAST(AVG(a.units_sold) AS decimal(10,2)) AS avg_units_sold
FROM cleaned_analytics AS a
JOIN cleaned_sessions AS cl
ON a.visitid = cl.visit_id
WHERE a.units_sold IS NOT NULL
GROUP BY cl.city
ORDER BY avg_units_sold DESC


Answer:

TOP 5 PRODUCTS ORDERED AVERAGES GROUPED BY CITIES

1-CHICAGO 5.00
2-PITTSBURG 4.00
3-NEW YORK 3.82 
4-HOUSTON 2.5
5-TORONTO 2.33

THE TOP 5 PRODCTS ORDERED AVERAGES GROUPED BY COUNTRY
1-CANADA
2-UNITED STATES
3-BULGARIA
4-MEXICO
5-JAPAN

**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries: 

CREATE TEMPORARY TABLE country_counts AS (
  SELECT
    a.city,
    a.country,
    a.v2productcategory,
    COUNT(*) AS product_count,
    RANK() OVER (PARTITION BY a.country ORDER BY COUNT(*) DESC) AS rank
  FROM
    products p
  JOIN
    all_sessions a ON p.sku = a.productsku
  GROUP BY
    a.city,
    a.country,
    a.v2productcategory
);

---query to search product category by country
SELECT
  country,
  v2productcategory,
  product_count,
  rank
FROM
  country_counts
WHERE
  rank = 1
ORDER BY
  product_count DESC, country
  ---query search for product category based on city
  SELECT
  city,
  v2productcategory,
  product_count,
  rank
FROM
  country_counts
WHERE
  rank = 1
ORDER BY
  product_count DESC, city



Answer:

TOP 5 COUNTRIES with the most 1 in product category sales is as below:

1-UNITED STATES 566 1st place rankings in product category
2- UNITED KINGDON 168 1st place rankings in product category
3- GERMANY 106 1st place rankings in product category
4- CANADA 85 1st place rankings in product category
5- INDIA 81 1st place rankings in product category

Based on that finding the United States has the most product sales by categories.

One thing that was noticed that in the top results one commonality was youtube as a product category result came up multiple times.



**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:

TOP 5 SOLD PRODUCTS BY CITY 

SELECT cl.city, cl.v2product_name, SUM(a.units_sold) AS total_units_sold
FROM cleaned_analytics AS a
JOIN cleaned_sessions AS cl
ON a.visitid = cl.visit_id
WHERE a.units_sold IS NOT NULL
GROUP BY cl.city, cl.v2product_name
ORDER BY total_units_sold DESC

TOP 5 SOLD PRODUCTS BY COUNTRY

SELECT cl.country, cl.v2product_name, SUM(a.units_sold) AS total_units_sold
FROM cleaned_analytics AS a
JOIN cleaned_sessions AS cl
ON a.visitid = cl.visit_id
WHERE a.units_sold IS NOT NULL
GROUP BY cl.country, cl.v2product_name
ORDER BY total_units_sold DESC


Answer:
TOP 5 SOLD PRODUCTS BY CITY

1- SUNNYVALE, SPF 15 SLIM & SLENDER LIP BALM, 168
2- NEW YORK, GOOGLE ALPINE STYLE BACKPACK, 164
3- CHICAGO, GOOGLE ALPINE STYLE BACKPACK, 164
4-MOUNTAINVIEW, GOOGLE MENS AIRFLOW 1/4 ZIP PULLOVER, 54
5- MOUNTAINVIEW, GRIP LIGHLIGHTER PEN 3 PACK, 50

TOP 5 SOLD PRODUCTS BY COUNTRY

1-UNITED STATES, GOOGLE ALPINE STYLE BACKPACK, 227
2- UNITED STATES, SPF-15 SLIM & SLENDER LIP BALM, 168
3- UNITED STATES, GOOGLES MEN AIRFLOW 1/4 ZIP PULLOVER, 56
4- UNITED STATES, GRIP HIGHLIGHTER PEN 3 PACK, 50
5- NEST PROTECT SMOKE + CO WHITE-WIRE ALARM USA, 28


BASED ON THESE RESULTS THE TOP SELLING PRODUCTS ARE FROM THE UNITED STATES AND THE "GOOGLE ALPINE STYLE BACKPACK"
IS THE MOST POPULAR PRODUCT BASED ON IT BEING THE TOP SOLD PRODUCT IN 2 SEPERATE CITIES AND THE NUMBER ONE BY COUNTRY.


**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:

SUMMARY TABLE OF COUNTRY AND TOTAL REVENUE 

SELECT cl.country, SUM(a.units_sold * cl.product_price) AS total_revenue
FROM cleaned_analytics AS a
JOIN cleaned_sessions AS cl
ON a.visitid = cl.visit_id
WHERE a.units_sold IS NOT NULL
GROUP BY cl.country
ORDER BY cl.country ASC 

SUMMARY TABLE OF CITIES AND TOTAL REVENUE


SELECT cl.city, cl.country, SUM(a.units_sold * cl.product_price) AS total_revenue
FROM cleaned_analytics AS a
JOIN cleaned_sessions AS cl
ON a.visitid = cl.visit_id
WHERE a.units_sold IS NOT NULL
GROUP BY cl.city, cl.country
ORDER BY cl.city ASC

Answer:

The Top 3 cities with the greatest impact on revenue generated are "not set" this could mean multiple things and would require further diagnoses in order to determine a more conclusive result.





