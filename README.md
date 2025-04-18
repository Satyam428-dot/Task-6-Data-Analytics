# Task-6-Data-Analytics
### Extracting Date Information
The column Order Date is stored as text, so STR_TO_DATE() converts it into a proper date format (%Y-%m-%d = Year-Month-Day).
EXTRACT(YEAR) and EXTRACT(MONTH) pull the year and month parts from the converted date for grouping and analysis
### Calculating Total Revenue
Adds up all the values from the Sales Price column to calculate total revenue.
### Counting Unique Orders
Counts distinct Order ID values to determine the number of unique orders placed.
### Filtering the Date Range
Filters the rows to include only orders placed between January 1, 2023, and December 31, 2024.
### Grouping and Aggregating
Groups the results by year and month. Aggregations like SUM and COUNT are applied within each group.
## Code- 
SELECT
    EXTRACT(YEAR FROM STR_TO_DATE(`Order Date`, '%Y-%m-%d')) AS year,
    EXTRACT(MONTH FROM STR_TO_DATE(`Order Date`, '%Y-%m-%d')) AS month,
    SUM(`Sales Price`) AS total_revenue,
    COUNT(DISTINCT `Order ID`) AS order_volume
FROM
    sales.sales
WHERE
    STR_TO_DATE(`Order Date`, '%Y-%m-%d') >= '2023-01-01'
    AND STR_TO_DATE(`Order Date`, '%Y-%m-%d') < '2025-01-01'
GROUP BY
    EXTRACT(YEAR FROM STR_TO_DATE(`Order Date`, '%Y-%m-%d')),
    EXTRACT(MONTH FROM STR_TO_DATE(`Order Date`, '%Y-%m-%d'))
ORDER BY
    year,
    month;
