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




Question 2: 

SQL Queries:

Answer:



Question 3: 

SQL Queries:

Answer:



Question 4: 

SQL Queries:

Answer:



Question 5: 

SQL Queries:

Answer:
