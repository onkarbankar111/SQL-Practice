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
insert into employee values(3,'Vikas',100,12000,4,37);
insert into employee values(4,'Rohit',100,5000,2,16);
insert into employee values(5,'Mudit',200,12000,6,55);
insert into employee values(6,'Agam',200,10000,2,14);
insert into employee values(7,'Sanjay',200,9000,2,13);
insert into employee values(8,'Ashish',200,5000,2,12);
insert into employee values(9,'Mukesh',300,6000,6,51);
insert into employee values(10,'Rakesh',500,7000,6,50);
SELECT * FROM employee

--Write a SQL to print employee details whose employee salary is more than their department avgerage salary 

--Independent Subquery

SELECT e.*, d.avg_dep_salary
FROM employee e
inner join
(SELECT dept_id, avg(salary) as avg_dep_salary 
from employee
group by dept_id) d
on e.dept_id = d.dept_id
WHERE e.salary > d.avg_dep_salary

--Corelated Subquery 

SELECT * FROM employee e1
WHERE salary > (SELECT avg(e2.salary) FROM employee e2 
                WHERE e1.dept_id = e2.dept_id)

```
