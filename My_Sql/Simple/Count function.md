* Count function :- count(*) ,count(0),count(-1),count('onkar') all of them give same result.

```SQL
  create table emp (
  emp_id int,
  emp_name varchar(20),
  salary int,
  manager_id int,
  emp_age int,
  dep_id int,
  dep_name varchar(10),
  gender varchar(20)
  )
insert into emp values (1,'Ankit',10000,4,39,100,'Analytics','Female'),
(2,'Mohit',15000,4,48,100,'IT','Male'),(3,'Vikas',10000,4,37,100,'Analytics','Female'),
(4,'Rohit',5000,4,16,100,'Analytics','Female'),(5,'Mudit',12000,4,55,200,'IT','Male'),
(6,'Agam',12000,4,14,200,'IT','Male'),(7,'Sanjay',9000,4,13,200,'IT','Male'),
(8,'Ashish',5000,4,12,200,'IT','Male'),(9,'Mukesh',6000,4,51,300,'HR','Male'),
(10,'Rakesh',7000,4,50,300,'HR','Male'),(11,'Akhil',3000,4,31,500,Null,'Male'),
(Null,Null,Null,Null,Null,Null,Null,Null)
select * from emp

select count(*) from emp
--Output = 12 rows (count null value rows also i.g count all rows in the table)

select count(*) ,count(0),count(-1), count('onkar') from emp
--Output = 12 rows (All of them gives same result)

select count(dep_name) from emp
--Output = 10 rows (In this case ignore the null values)

select count(distinct dep_name) from emp
--Output = 3 rows (In this case shows only distinct values of columns and ignore the null values)
```
