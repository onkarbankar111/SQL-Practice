NTILE Analytic Function :- NTILE fuction is used for grouping of rows based on the finding of percentage 
and number of rows.

Concept:-  suppose total 800 rows in the orders table and we want to find top 25% and bottom 25% rows.  then the output expected 400 rows.  
If we have 800 rows then we can divide this rows into 4 parts i.g NTILE(4)


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
-- In this case first filter on top 16 records. and then divide 16 records into 4 groups of same number of rows

with cte as (
SELECT top 16 customet_name, sum(sales) as total_sales 
FROM orders 
group by customer_name
order by total_sales desc)
select * from (SELECT *
, NTILE (4) over (order by total_sales desc) as cust_groups
from cte) a  where cust_groups = 1 or cust_groups = 4
-- Top 25% and bottom 25%

--Scenario-2]
with cte as (
SELECT top 18 customet_name, sum(sales) as total_sales 
FROM orders 
group by customer_name
order by total_sales desc)
SELECT *
, NTILE (4) over (order by total_sales desc) as cust_groups
from cte
-- In this case first filter on top 18 records. and then divide 18 records into 4 groups
-- first two groups having 5 rows and last two groups having 4 rows.

--Scenario-3]
with cte as (
SELECT customet_name, region, sum(sales) as total_sales 
FROM orders 
group by customer_name, region)
SELECT *
, NTILE (4) over (partition by region order by total_sales desc) as cust_groups
from cte
```
