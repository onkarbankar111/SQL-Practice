* Update statement :-

  Update and Alter both are different things

Update- Update statement is used to update the data(Updating the row). Update statement cannot
used to update column structure or table structure.

Alter :- Alter statement is used to update the column structure or table structure.
i.g we want to add or delete the column, we want to update the datatype of column
```SQL
create table emp (
  emp_id int,
  emp_name varchar(20),
  salary int,
  manager_id int,
  emp_age int,
  dep_id int 
  )
insert into emp values (1,'Ankit',10000,4,39,100),
(2,'Mohit',15000,4,48,100),(3,'Vikas',10000,4,37,100),(4,'Rohit',5000,4,16,100),
(5,'Mudit',12000,4,55,200),(6,'Agam',12000,4,14,200),(7,'Sanjay',9000,4,13,200),
(8,'Ashish',5000,4,12,200),(9,'Mukesh',6000,4,51,300),(10,'Rakesh',7000,4,50,300),
(11,'Akhil',3000,4,31,500)
select * from emp
```
1- Update basic syntax
```SQL
update emp set salary = 12000
--In this case update the salary column value for all rows
```
2- Update with where clause
```SQL
update emp set salary = 12000 where emp_id = 1
update emp set salary = 12000 where emp_age >30
--In this case update the salary value only for which satisfies the where condition.
```
3- Update multiple values 
```SQL
update emp set salary = 12000 , dep_id = 200 where emp_id=2
--In this case update the multiple values only for which satisfies the where condition.
```
4- Update using calculations (Col calculation / case when)
```SQL
update emp set salary =salary + 1000
--In this case update the salary column for each rows having salary + 1000
update emp set salary = salary * 1.1 where emp_id=4
--In this case increase the salary of 10 % who has emp_id 4
update emp set salary = case when dep_id = 100 then salary * 1.1
                             when dep_id = 200 then salary * 1.2
                             else salary
                        end
```
5- Update using Join:-
```SQL
-- Create one more table dept
create table dept (
  dep_id int,
  dep_name varchar(20)
)
insert into dept values (100,'Analytics'),
(200,'IT'),(300,'HR'),(400,'Text Analytics')
select * from dept
alter table emp add dep_name varchar(20)
select * from emp

update emp set dep_name=d.dep_name from emp e 
left join dept d
on e.dep_id = d.dep_id
```
6- Interview question on Update
```SQL
select * from emp
alter table emp add gender varchar(10)
select * from emp
update emp set gender = case when dep_id = 100 then 'Male' else 'Female' end
select * from emp
--Swab the gender 
Update emp set gender = case when gender = 'Male' then 'Female' else 'Male' end
select * from emp
```
**7- cautious before running an update statement
```SQL
select *, swab = case when gender = 'Male' then 'Female' else 'Male' end from emp
```
