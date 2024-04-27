NTILE Analytic Function :- NTILE fuction is used for grouping of rows based on the finding of percentage 
and number of rows.


Q] Find top 25 and bottom 25 percent customers by sales.

Solution:-
```SQL
--Scenario-1]
with cte as (
SELECT top 16 customet_name, sum(sales) as total_sales 
FROM orders 
group by customer_name
order by total_sales desc)
SELECT *
, NTILE (4) over (order by total_sales desc) as cust_groups
from cte

--Scenario-2]
with cte as (
SELECT top 18 customet_name, sum(sales) as total_sales 
FROM orders 
group by customer_name
order by total_sales desc)
SELECT *
, NTILE (4) over (order by total_sales desc) as cust_groups
from cte

--Scenario-3]
with cte as (
SELECT customet_name, region, sum(sales) as total_sales 
FROM orders 
group by customer_name, region)
SELECT *
, NTILE (4) over (partition by region order by total_sales desc) as cust_groups
from cte
```
