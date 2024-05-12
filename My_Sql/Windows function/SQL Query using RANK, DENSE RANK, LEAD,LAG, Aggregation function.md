```SQL
create table employee
( emp_ID int
, emp_NAME varchar(50)
, DEPT_NAME varchar(50)
, SALARY int);

insert into employee values(101, 'Mohan', 'Admin', 4000);
insert into employee values(102, 'Rajkumar', 'HR', 3000);
insert into employee values(103, 'Akbar', 'IT', 4000);
insert into employee values(104, 'Dorvin', 'Finance', 6500);
insert into employee values(105, 'Rohit', 'HR', 3000);
insert into employee values(106, 'Rajesh',  'Finance', 5000);
insert into employee values(107, 'Preet', 'HR', 7000);
insert into employee values(108, 'Maryam', 'Admin', 4000);
insert into employee values(109, 'Sanjay', 'IT', 6500);
insert into employee values(110, 'Vasudha', 'IT', 7000);
insert into employee values(111, 'Melinda', 'IT', 8000);
insert into employee values(112, 'Komal', 'IT', 10000);
insert into employee values(113, 'Gautham', 'Admin', 2000);
insert into employee values(114, 'Manisha', 'HR', 3000);
insert into employee values(115, 'Chandni', 'IT', 4500);
insert into employee values(116, 'Satya', 'Finance', 6500);
insert into employee values(117, 'Adarsh', 'HR', 3500);
insert into employee values(118, 'Tejaswi', 'Finance', 5500);
insert into employee values(119, 'Cory', 'HR', 8000);
insert into employee values(120, 'Monica', 'Admin', 5000);
insert into employee values(121, 'Rosalin', 'IT', 6000);
insert into employee values(122, 'Ibrahim', 'IT', 8000);
insert into employee values(123, 'Vikram', 'IT', 8000);
insert into employee values(124, 'Dheeraj', 'IT', 11000);
SELECT * FROM employee

--Q] Maximum salary of employee
SELECT max(salary) as max_salary FROM employee

SELECT e.* ,
max(salary) over() as max_salary
from employee e
--In this case add new column as max_salary and all rows having max salary

--Q] Department wise maximun salaried employee 
SELECT dept_name, max(salary) as max_salary 
FROM employee 
GROUP BY dept_name 

SELECT e.* ,
max(salary) over(partition by dept_name) as max_salary
from employee e

--row_number, rank, dense_rank, lead and lag 

SELECT e.* ,
row_number() over() as rn
from employee e

SELECT e.* ,
row_number() over(partition by dept_name) as rn
from employee e


--Q] Fetch the first 2 employees from each department to join the company. 
SELECT * FROM (
  SELECT e.* ,
  row_number() over(partition by dept_name ORDER BY emp_id) as rn
  from employee e) x
WHERE x.rn < 3 

--Rank
--Q] Fetch the top 3 employee in each department earning max salary 
SELECT * FROM (
  SELECT e.* ,
  rank() over(partition by dept_name ORDER BY salary desc) as rnk
  from employee e) x
WHERE x.rnk < 4


--Rank, dense_rank,row_number 
  SELECT e.* ,
  rank() over(partition by dept_name ORDER BY salary desc) as rnk,
  dense_rank() over(partition by dept_name ORDER BY salary desc) as dense_rnk,
  row_number() over(partition by dept_name ORDER BY salary desc) as rn
  from employee e 
  
--LEAD() & LAG() 
--Q] Fetch the query to display if the salary of employee is higher, lower or equal to previous emplyeee 
SELECT * ,
lag(salary) over (partition by dept_name ORDER by emp_id) as previous_emp_salary
lag(salary) over (partition by dept_name ORDER by emp_id) as next_emp_salary
FROM employee

SELECT * ,
lag(salary,2,0) over (partition by dept_name ORDER by emp_id) as previous_emp_salary
--Second previous salary
lag(salary,2,0) over (partition by dept_name ORDER by emp_id) as next_emp_salary
--second next salary
FROM employee


SELECT e.* ,
lag(salary) over (partition by dept_name ORDER by emp_id) as previous_emp_salary,
case when e.salary > lag(salary) over (partition by dept_name ORDER by emp_id) then 'Higher than previous employee',
case when e.salary < lag(salary) over (partition by dept_name ORDER by emp_id) then 'Lower than previous employee',
case when e.salary = lag(salary) over (partition by dept_name ORDER by emp_id) then 'Same as previous employee'
end as salary_range
FROM employee e
```
