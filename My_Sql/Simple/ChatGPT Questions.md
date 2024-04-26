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
insert into employee values(10,'Rakesh',700,7000,6,50);
insert into employee values(11,'Ramesh',300,8000,6,52);
SELECT * FROM employee

--Q-1]Write a SQL to give highest salaried employee 
SELECT emp_name, salary FROM employee order by salary desc 
LIMIT 1;
--           OR
SELECT emp_name, salary from employee
where salary = (SELECT max(salary) from employee)
--      OR 
with cte as (
select emp_name, salary, row_number() over (order by salary desc) as rn from employee)
select * from cte where rn = 1

--Q-2] Write a SQL to give second highest salaried employee
with cte as (
select emp_name, salary, row_number() over (order by salary desc) as rn from employee)
select * from cte where rn = 2
--           OR 
SELECT emp_name, salary from employee
where salary = (select max(salary) FROM employee where salary not in (SELECT max(salary) from employee))

--Q-3]Write a SQL to give highest salaried employee in each department 
with cte as (
SELECT *, 
row_number() over (partition by dept_id order by salary desc) as rn
from employee
)
SELECT dept_id, salary, rn FROM cte where rn = 1
--             OR 
SELECT e1.emp_name, e1.dept_id, e1.salary 
from employee e1
WHERE (e1.dept_id, e1.salary) IN (SELECT dept_id, max(salary)   
                                  FROM employee 
GROUP by dept_id);

--Q-4] Write a sql to give details of top 5 selling products 
with cte as (
SELECT product_name, sum(quantity) as total_quantity, 
row_number() over (ORDER by sum(quantity) desc) as rn
from sales GROUP by product_name)
SELECT product_name, total_quantity from cte WHERE rn <= 5 
--     OR 
SELECT product_name, sum(quantity) as total_quantity
from sales 
GROUP by product_name
ORDER by sum(quantity) desc
LIMIT 5

--Q-5]Write a SQL to find TOP 5 and BOTTOM 5 products by sales 

with cte as (
SELECT product_name, sum(quantity) as total_quantity, 
row_number() over (ORDER by sum(quantity) desc) as top_rn,
row_number() over (ORDER by sum(quantity) Asc) as bottom_rn,
from sales GROUP by product_name)
SELECT product_name, total_quantity from cte
where top_rn <= 5 or bottom_rn <= 5
order by top_rn, bottom_rn
--                 OR 
SELECT product_name, sum(quantity) as total_quantity
from sales 
GROUP by product_name
ORDER by sum(quantity) desc
LIMIT 5
UNION
SELECT product_name, sum(quantity) as total_quantity
from sales 
GROUP by product_name
ORDER by sum(quantity) asc
LIMIT 5

```
