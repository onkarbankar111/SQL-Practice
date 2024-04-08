*RANK, DENSE_RANK,ROW_NUMBER:-

```SQL
create table emp (
  emp_id int,
  emp_name varchar(20),
  department_id int,
  salary int
  )
insert into emp values (1,'Ankit',100,10000),
(2,'Mohit',100,15000),(3,'Vikas',100, 10000),(4,'Rohit',100, 5000),
(5,'Mudit',200, 12000),(6,'Agam',200, 12000),(7,'Sanjay',200, 9000),
(8,'Ashish',200, 5000)
select * from emp
```

* Concept:-

we have to calculate the RANK and DENSE_RANK based on salary of above example(8 records in the above example)

ROW_NUMBER:-1,2,3,4,5,6,7,8

RANK:-1,2,2,4,4,6,7,7

DENSE_Rank:-1,2,2,3,3,4,5,5

```SQL
--calculate the RANK and DENSE_RANK based on salary
select emp_id, emp_name, department_id, salary,
rank() over (order by salary desc) as rnk,
dense_rank() over (order by salary desc) as dense_rnk,
row_number() over (order by salary desc) as rn
from emp

--calculate the RANK and DENSE_RANK partition by department_id and order by salary
select emp_id, emp_name, department_id, salary,
rank() over (partition by department_id order by salary desc) as rnk,
dense_rank() over (partition by department_id order by salary desc) as dense_rnk,
row_number() over (partition by department_id order by salary desc) as rn
from emp

--Interview question
--Calculate highest salary of each department
select * from (select emp_id, emp_name, department_id, salary,
rank() over (partition by department_id order by salary desc) as rnk
from emp) a 
where rnk=1
--                  or
with cte as (
select emp_id, emp_name, department_id, salary,
rank() over (partition by department_id order by salary desc) as rnk
from emp) 
select * from cte where rnk=1
```


