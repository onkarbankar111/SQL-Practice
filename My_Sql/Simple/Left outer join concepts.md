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
(8,'Ashish',5000,4,12,200),(9,'Mukesh',6000,4,51,300),(10,'Rakesh',7000,4,50,500)
select * from emp

create table dept (
  dep_id int,
  dep_name varchar(20)
)
insert into dept values (100,'Analytics'),
(200,'IT'),(300,'HR'),(400,'Text Analytics')
select * from dept

SELECT * FROM emp 
left join dept
on emp.dep_id = dept.dep_id

SELECT * FROM emp 
inner join dept
on emp.dep_id = dept.dep_id
--Only the records shows which satisfies the join comdition

SELECT * FROM emp 
left join dept
on emp.dep_id = dept.dep_id and dept.dep_name='Analytics'
--In this case first filter the dept table and then apply the join condition
--                 OR
SELECT * FROM emp 
left join (select * from dept where dep_name='Analytics') dept
on emp.dep_id = dept.dep_id 

SELECT * FROM emp 
left join dept
on emp.dep_id = dept.dep_id 
where dept.dep_name='Analytics'
--In this case first apply the join condition and then filter where condition

--Interview question
--Find out the employee whose department is not present in department table
SELECT * FROM emp 
left join dept
on emp.dep_id = dept.dep_id 
where dep_name is null


SELECT * FROM emp 
left join dept
on emp.dep_id = dept.dep_id and emp.salary=10000
--In this case first filter the emp table and then apply the join condition

SELECT * FROM emp 
left join dept
on emp.dep_id = dept.dep_id 
where emp.salary=10000
--In this case first apply the join condition and then filter where condition
```
