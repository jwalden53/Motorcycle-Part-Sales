# Short Description 
For this project, I am analyzing data for a motorcycle parts company to better understand their revenue streams. I am creating a query to calculate net revenue generated across various product lines, segmented by date and warehouse location.

# Read Me
-- Project: Analyzing Wholesale Revenue for a Motorcycle Parts Company

-- Project Details:
-- Objective: Calculate net revenue for each product line, filtered exclusively for 'Wholesale' orders, grouped by month and warehouse.
-- Expected Output Format:
-- | product_line | month   | warehouse | net_revenue |

-- SQL Code:
SELECT 
    product_line,
    TO_CHAR(date, 'Month') AS month,
    warehouse,
    (SUM(total) - SUM(payment_fee)) AS net_revenue
FROM sales
WHERE client_type = 'Wholesale'
GROUP BY product_line, TO_CHAR(date, 'Month'), warehouse
ORDER BY product_line, TO_CHAR(date, 'Month'), (SUM(total) - SUM(payment_fee)) DESC;

-- Query Explanation:
-- 1. Filters records for 'Wholesale' orders.
-- 2. Groups data by product_line, month (formatted as a textual month), and warehouse.
-- 3. Calculates net revenue by subtracting the sum of payment fees from the sum of total revenue.
-- 4. Orders the output by product line, month, and descending net revenue.

-- Sample Query Result:
-- | product_line     | month     | warehouse | net_revenue |
-- | ---------------- | --------- | --------- | ----------- |
-- | product_one      | June      | North     | 15000.00    |
-- | product_one      | July      | Central   | 12000.50    |
-- | product_two      | June      | West      | 9000.00     |
-- | product_three    | August    | North     | 8000.75     |
-- | product_two      | July      | Central   | 7500.00     |
