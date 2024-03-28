```SQL
create table emp (
  emp_id int,
  emp_name varchar(50),
  salary int,
  manager_id int
);

insert into emp values (1, 'Ankit', 10000, 4),(2, 'Mohit', 15000, 5),(3, 'Vikas', 10000, 4),
(4, 'Rohit', 5000, 2),(5, 'Mudit', 12000, 6),(6, 'Agam', 12000, 2),(7, 'Sanjay', 9000, 2),
(8, 'Ashish', 5000, 2)

select * from emp
```

Q]find the employees with salay more than their manager salary

Self Join - Joining a table with itself is called as self join.

Inner Join - Returns all the rows from both participating tables that satisfy the join condition.

```SQL
select e.emp_id, e.emp_name, m.emp_name as manager_name, e.salary, m.salary as manager_salary
from emp e 
inner join emp m 
on e.manager_id = m.emp_id
where e.salary > m.salary
```
