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

--The first and last value function without using order by then shows error

--First value function]

SELECT *, first_value(emp_name) over (ORDER by salary) as lowest_emp_salary
FROM employee

SELECT *, first_value(emp_name) over (ORDER by emp_age) as youngest_emp
FROM employee

SELECT *, first_value(emp_name) over (partition by dept_id ORDER by emp_age) 
as youngest_emp_each_dept
FROM employee

SELECT *, first_value(emp_name) over (partition by dept_id ORDER by emp_age desc) 
as oldest_emp_each_dept
FROM employee

--Last value function]
```
