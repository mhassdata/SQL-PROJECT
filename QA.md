What are your risk areas? Identify and describe them.
Data Type
Purpose: Check that the data matches the data type defined for a field.
Example: Data values for unit_price must be a numeric data type instead of string
Script: 
Describe Table sales_report;
Alter table sales_report alter column unit_price type integer
Limitations: The data values of 1,000,000 would pass the data type validation as it’s still numeric but would be an unacceptable value as a unit_price is too high. For this case, data range validation is also needed.
Data Range
Purpose: Check that the data falls within an acceptable range of values defined for the field.
Example: checking that the sentiment score is between a min and max value. In this case between -1 and 1
Script: select distinct sentimentscore from sales_report
Limitations: A data value that would fall out of this range such as -10. It would not fall in the data range but would pass as a numeric data type check. For this case, data constraint validation is also needed.
Data Constraints
Purpose: Check that the data meets certain conditions or criteria for a field. This includes the type of data entered as well as other attributes of the field, such as number of characters. 
Example: unit_price number of decimals constraint: Data values for price must be limited to 2 decimal places to replicate dollar value.
Script: CAST(unit_price type as decimal(10,2)
Limitations: The data value outside of this is a numeric value and would pass the data type validation, but, it would need to be adjusted as vale’s are in the millions.
Data Consistency
Purpose: Check that the data makes sense in the context of other related data.
Example: Data values for dates can’t be enter in a future date of today. Must be accurate to when the transaction occurred.
Select distinct date from all_sessions where date < ‘2023-06-14’
Limitations: Data might be consistent but still incorrect or inaccurate due to wrong date format entered. 
