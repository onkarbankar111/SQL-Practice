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
```
