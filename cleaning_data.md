What issues will you address by cleaning the data?

During the cleaning process there were empty values in entire columns and due to this initial issue i had to make the decision to remove columns with no values.

there was no distinct relationship between particular tables and due to this i had to alter the tables based on these findings

attempted to connect tables using product sku as some tables had more product skus then others this left out large volumes of data from tables



Queries:
FIRST CREATED 5 TABLES
SECOND IMPORT CSV FILE ONTO PGADMIN


AND THEN DUPLICATED EACH TABLE 

CREATE TABLE all_sessions2 AS
SELECT *
FROM all_sessions

CREATE TABLE analytics2 AS 
SELECT *
FROM analytics

CREATE TABLE products2 AS 
SELECT *
FROM products

CREATE TABLE sales_by_sku2 AS 
SELECT *
FROM sales_by_sku

CREATE TABLE sales_report2 AS 
SELECT *
FROM sales_report


—REMOVING COLUMNS WITH ALL NULL VALUES

ALTER TABLE cleaned_sessions
DROP COLUMN product_refund_amt,
DROP COLUMN product_quantity,
DROP COLUMN product_revenue,
DROP COLUMN item_revenue,
DROP COLUMN total_transaction_revenue,
DROP COLUMN transactions
DROP COLUMN ecommerceaction_option


—REMOVING COLUMNS WITH ALL NULL VALUES 

ALTER TABLE analytics2
DROP COLUMN userid,
DROP COLUMN revenue,
DROP COLUMN timeonsite 

—REMOVING ROWS WITH NULL VALUES 

DELETE FROM products2
WHERE sentimentscore IS NULL
AND sentimentmagnitude IS null

—RENAMED TABLE NAME AFTER REMOVING NULL VALUES

ALTER TABLE analytics2 RENAME TO cleaned_analytics


--CHECKING FOR NULL VALUE 
SELECT full_visitor_id
FROM cleaned_sessions 
WHERE full_visitor_id =' ' OR full_visitor_id IS NULL

--updating column from seconds to minutes
ALTER TABLE cleaned_sessions
ALTER COLUMN time TYPE numeric 
USING time::numeric/60

--THERE ARE 14223 DISTINCT ROWS FOR FULL_VISITOR_ID
SELECT DISTINCT full_visitor_id
FROM cleaned_sessions

--THERE ARE 536 DISTINCT ROWS FOR PRODUCT_SKU
SELECT DISTINCT product_sku
FROM cleaned_sessions


--there are 2 distinct types for type 
SELECT DISTINCT type
FROM cleaned_sessions

--there are 471 product names for cleaned_sessions
SELECT DISTINCT v2product_name
FROM cleaned_sessions

--there are 74 product category types
SELECT DISTINCT v2product_category
FROM cleaned_sessions


—the most purchased unit price is 18 dollars based on that we can assume a large volume of sales come from lower end products

SELECT DISTINCT unitprice/1000000 as unit_price, count(*) as c1
FROM cleaned_analytics
GROUP BY unit_price
order by c1 desc;


—COLUMN REMOVED item_quantity

ALTER TABLE cleaned_sessions
DROP COLUMN item_quantity
