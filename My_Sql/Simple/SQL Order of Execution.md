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
insert into employee values(8,'Ashish',200,7000,2,12);
insert into employee values(9,'Mukesh',300,6000,6,51);
insert into employee values(11,'Ramesh',300,8000,6,52);
SELECT * FROM employee

select * from employee where salary > 6000

--Order of Execution :- From -> where -> select

select emp_id, emp_name, salary, (salary*1.0)/2 as half_salary 
from employee 
where salary > 6000
order by half_salary desc

--From -> Where -> Select -> Order by

Select TOP 5 emp_id, emp_name, salary, (salary*1.0)/2 as half_salary 
from employee 
where salary > 6000
order by half_salary desc

-- From -> Where -> Select -> Order by -> Top 5

-- Top 5 and Limit 5 having same meaning. Which command used in both depends on database
-- In MS SQL database Top command is used.

select dept_id, sum(salary) as dep_salary
from employee 
where salary > 6000
GROUP by dept_id
order by dep_salary desc

-- From -> Where -> Group by -> Select -> Order by -> Top 5

select Top 1 dept_id, sum(salary) as dep_salary
from employee 
where salary > 6000
GROUP by dept_id
HAVING sum(salary) > 10000
order by dep_salary desc

-- From -> Where -> Group by -> Having -> Select -> Order by -> Top 1
```
