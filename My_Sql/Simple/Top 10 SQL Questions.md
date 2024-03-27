```SQL
create table emp(
emp_id int,
emp_name varchar(20),
department_id int,
salary int,
manager_id int,
)

insert into emp
values
(1, 'Ankit', 100,10000, 4),
(2, 'Mohit', 100, 15000, 5),
(3, 'Vikas', 100, 10000,4),
(4, 'Rohit', 100, 5000, 2),
(5, 'Mudit', 200, 12000, 6),
(6, 'Agam', 200, 12000, 2),
(7, 'Sanjay', 200, 9000, 2),
(8, 'Ashish', 200,5000,2),
(1, 'Saurabh',900,12000,2)
SELECT * from emp;
```
Q-1) How to find duplicates in a given table
```SQL
select emp_id, count(1) from emp group by emp_id having count(1) > 1
```
Q-2)How to delete duplicates
```SQL
--Create one more table same as emp
select *
into emp1
from emp
select * from emp1
--Delete duplicate in emp1 
--Step-1
select * , row_number() over (partition by emp_id order by emp_id) as rn from emp1
--step-2
with cte as (
  select * , row_number() over (partition by emp_id order by emp_id) as rn from emp1)
  delete from cte where rn>1
--Now deleted duplicate in emp1
select * from emp1
```
Q-3)Difference between union and union all 

Union - Combines the results of two or more select statement by eliminating duplicate rows.

Union all - Combines the results of two or more select statement by including duplicate rows.
```SQL
select manager_id from emp
UNION
select manager_id from emp1

select manager_id from emp
UNION all
select manager_id from emp1
```
Q-4) Employees who are not present in department table. 
```SQL
create table dept (
  dep_id int,
  dep_name varchar(20)
)
insert into dept values (100, 'Analytics'),(300,'IT')
select * from dept
select * from emp
--Method-1]
select * from emp where department_id not in (select dep_id from dept)
--Method-2]
select emp.* from emp left join dept 
on emp.department_id = dept.dep_id
where dept.dep_id is null
```
Note - Subquery not get the good performance so method 2 is better to use than method 1


Q-5]How to find second highest salary in each dept 

In this example we want to find second highest rank based on salary in each dept

eg if rank() - 1,1,3,4,5,5,7 then dense_rank() - 1,1,2,3,4,4,5

--select emp.*, rank() over (partition by department_id order by salary desc) as rn from emp
```SQL
with cte as (
select emp.*, dense_rank() over (partition by department_id order by salary desc) as rn from emp)
select * from cte where rn=2
--           OR
select * from (select emp.*, dense_rank() over (partition by department_id order by salary desc)
as rn from emp) as a 
where rn = 2
```
Q-6] Find all transactions done by shilpa
```SQL
Create table orders (
  customer_name varchar(20),
  order_date varchar(20),
  order_amount int,
  customer_gender Varchar(20)
  )
  insert into orders values ('Shilpa', '2020-01-01',10000,'Male'),('Rahul', '2020-01-02',12000,'Female'),
  ('SHILPA', '2020-01-02',12000,'Male'),('Rohit', '2020-01-03',15000,'Female'),
  ('shilpa', '2020-01-03',14000,'Male')
  select * from orders;
  
 select * from orders where upper(customer_name) = 'SHILPA'
 ```
Q-7] Update query to swab gender
```SQL
  select * from orders;
  
  update orders set customer_gender = case when customer_gender = 'Male' then 'Female' 
                                           when customer_gender = 'Female' then 'Male' end
```
