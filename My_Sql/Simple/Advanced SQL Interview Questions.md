```SQL
create table employee(
    emp_id int,
    emp_name varchar(20),
    dept_id int,
    salary int,
    manager_id int,
    emp_age int
);

insert into employee values(1,'Ankit',100,10000,4,39);
insert into employee values(2,'Mohit',100,15000,5,48);
insert into employee values(3,'Vikas',100,10000,4,37);
insert into employee values(4,'Rohit',100,5000,2,16);
insert into employee values(5,'Mudit',200,12000,6,55);
insert into employee values(6,'Agam',200,12000,2,14);
insert into employee values(7,'Sanjay',200,9000,2,13);
insert into employee values(8,'Ashish',200,5000,2,12);
insert into employee values(9,'Mukesh',300,6000,6,51);
insert into employee values(10,'Rakesh',500,7000,6,50);
insert into employee values(11,'dummy',400,4000,4,99);
SELECT * FROM employee

--Q] Find top 2 highest salaried  employee for each department 
with cte as (
SELECT * ,
row_number() over (partition by dept_id order by salary desc) as rn,
--dense_rank() over (partition by dept_id order by salary desc) as rn_dense
from employee )
SELECT * from cte where rn <= 2

--Q] Top 5 products by sales 
with cte as (
SELECT product_id, sum(sales) as sales 
from orders
GROUP by product_id
) 
SELECT top 5 product_id, sales 
FROM cte 
order by sales DESC 

--Q] Find each category of top 5 product_id 
with cte as (
SELECT category, product_id, sum(sales) as sales 
from orders
GROUP by category, product_id
) 
SELECT * from (SELECT *, 
row_number() over (partition by category ORDER BY sales desc) as rn 
FROM cte) a 
WHERE rn <= 5

--LEAD / LAG Function

-- Q] Year over year growth/products with current year comparison than previous year sale 
--Concept :- 
--2020 - 100 - 0% growth
--2021 - 200 - 100% growth
--2022 - 300 - 50% growth

WITH cte as (
SELECT year(order_date) as year_order, sum(sales) as sales
from orders 
GROUP by year(order_date)
--ORDER by year(order_date)
)
, cte2 as (
SELECT *,
lag(sales,1,sales) over (order by year_order) as previous_year_sales
FROM cte
)
SELECT *,
(sales-previous_year_sales)*100/previous_year_sales as yoy 
FROM cte2 

-- Q] Year over year growth in each category 
WITH cte as (
SELECT category, year(order_date) as year_order, sum(sales) as sales
from orders 
GROUP by category, year(order_date)
--ORDER by category, year(order_date)
)
, cte2 as (
SELECT *,
lag(sales,1,sales) over (partition by category order by year_order) as previous_year_sales
FROM cte
)
SELECT *,
(sales-previous_year_sales)*100/previous_year_sales as yoy 
FROM cte2 

--Q] running/cumulative sales year wise 
--Concept:- 
-- year  sales   running sum
--2020 - 100 - 100 
--2021 - 200 - 300   (100+200)
--2022 - 300 - 600   (100+200+300)
--2023 - 400 - 1000  (100+200+300+400)
--Q] running/cumulative sales year wise 
--Concept:- 
-- year  sales   running sum
--2020 - 100 - 100 
--2021 - 200 - 300   (100+200)
--2022 - 300 - 600   (100+200+300)
--2023 - 400 - 1000  (100+200+300+400)

WITH cte as (
SELECT year(order_date) as year_order, sum(sales) as sales
from orders 
GROUP by year(order_date)
--ORDER by year(order_date)
) 
select *, 
sum(sales) over(order by year_order) as cumulative_sales
from cte
--Above cumulative sum concept applicable only for unique sale values otherwise showing wrong output

--Q] category wise cumulative sum 
WITH cte as (
SELECT category, year(order_date) as year_order, sum(sales) as sales
from orders 
GROUP by category, year(order_date)
--ORDER by category, year(order_date)
) 
select *, 
sum(sales) over(partition by category order by year_order) as cumulative_sales
from cte
--Above cumulative sum concept applicable only for unique sale values otherwise showing wrong output 

--Q] rolling 3 month sale (previous 2 months and current month)
WITH cte as (
SELECT year(order_date) as year_order,month(order_date) as month_order_date, sum(sales) as sales
from orders 
GROUP by year(order_date),month(order_date)
--ORDER by year(order_date),month(order_date)
) 
select *, 
sum(sales) over(order by year_order, month_order_date rows between 2 preceding and current row) as cumulative_sales
from cte
-- In this case no matter sales value is unique or not.
```
