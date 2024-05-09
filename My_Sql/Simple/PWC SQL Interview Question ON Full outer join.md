Input Tables:-  
source table:-	
Id	Name
1	A
2	B
3	C
4	D
![image](https://github.com/onkarbankar111/SQL-Practice/assets/164195447/80817a30-0380-4776-9c7c-4e592d8e50f9)

Target table:-	
Id	Name
1	A
2	B
4	X
5	F
![image](https://github.com/onkarbankar111/SQL-Practice/assets/164195447/4b3762ee-b3be-4337-a7d9-c0c89e9c129b)

Expected Output:-   
3	New in source
5	New in target
4	Mismatch
![image](https://github.com/onkarbankar111/SQL-Practice/assets/164195447/2bd38387-ebac-436a-ab34-777936f6188e)

Solution:-    

```SQL
create table source(id int, name varchar(5))
insert into source values(1,'A'),(2,'B'),(3,'C'),(4,'D')
create table target(id int, name varchar(5))
insert into target values(1,'A'),(2,'B'),(4,'X'),(5,'F')

SELECT * FROM source
SELECT * FROM target

--Method-1]
--Step-1]
select s.*, t.* FROM source s
full outer join target t 
on s.id = t.id
WHERE s.name != t.name

--Null is not comparable so this is not expected output

--Step-2]
select s.*, t.* FROM source s
full outer join target t 
on s.id = t.id
WHERE s.name is null or t.name is null or s.name != t.name

--Step-3] 
select coalesce(s.id, t.id) as id,
case when t.name is null then 'New in source' when s.name is null then 'New in target' 
else 'Mismatch' end as Comment FROM source s
full outer join target t 
on s.id = t.id
WHERE s.name is null or t.name is null or s.name != t.name
```
