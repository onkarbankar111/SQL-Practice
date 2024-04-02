Full outer Join :-Retrives all the rows from both tables.If a match is found then displays the matching rows,
if not it displays null value

** Deloitte interview question**

Input tables:- Two input tables emp_2020 & emp_2021

emp_2020:-	
emp_id	designation
1	Traniee
2	Developer
3	Senior Developer
4	Manager
	
![image](https://github.com/onkarbankar111/SQL-Practice/assets/164195447/b4c47e18-2a72-4445-8cb9-3f0a4020d8da)

emp_2021:-	
emp_id	designation
1	Developer
2	Developer
3	Manager
5	Traniee
![image](https://github.com/onkarbankar111/SQL-Practice/assets/164195447/e364e10e-587b-4fca-a80b-3dc3b780657c)

	
Expected Output:-
emp_id	comment
1	Promoted
3	Promoted
4	Resigned
5	New
![image](https://github.com/onkarbankar111/SQL-Practice/assets/164195447/0a9b7b26-d41a-432d-afc8-4de09b9d0bb0)


Solution:-
```sql
--Step-1]
select e20.*, e21.* from emp_2020 e20 
full outer join emp_2021 e21
on e20.emp_id = e21.emp_id

--Step-2]In second step we want to remove the employess having same designation in e20 & e21
select e20.*, e21.* from emp_2020 e20 
full outer join emp_2021 e21
on e20.emp_id = e21.emp_id
where e20.designation != e21.designation
--This is not expected result.Null values cannot compared.

select e20.*, e21.* from emp_2020 e20 
full outer join emp_2021 e21
on e20.emp_id = e21.emp_id
where isnull(e20.designation,'xyz') != isnull(e21.designation,'abc')
--This is expected result for step2

--Step-3]
select isnull (e20.emp_id, e21.emp_id),
case when e20.designation != e21.designation then 'Promoted'
when e20.designation is null then 'New'
else 'Resigned' end as comment
from emp_2020 e20
full outer join emp_2021 e21
on e20.emp_id = e21.emp_id
where isnull(e20.designation,'xyz') != isnull(e21.designation,'abc')
--Final output
```
