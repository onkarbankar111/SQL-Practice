```SQL
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
```
