Input and expected output		
	input	output
	a	Dup1
	a	Dup1
	b	Null
	c	Dup2
	c	Dup2
	c	Dup2
	d	Dup3
	d	Dup3
	e	Null
![image](https://github.com/onkarbankar111/SQL-Practice/assets/164195447/c0b1c9f9-afb8-438f-9886-6ebca8c1f9db)

Solution:-

```SQL
create table list (id varchar(5));
insert into list values ('a'),('a'),('b'),
('c'),('c'),('c'),('d'),('d'),('e')
select * from list

--step-1]
select id, count(id) from list group by id having count(id) > 1
--In this case removing the unique values that means showing duplicates

--step-2]
with cte_dups AS (
  select id , count(id) as cout from list group by id having count(id) > 1)
select *, rank() over (order by id asc) as rn from cte_dups
--In this case find the rank of eack ids in ascending order

--step-3]
with cte_dups AS (
  select id , count(id) as cout from list group by id having count(id) > 1)
, cte_rank as (
select *, rank() over (order by id asc) as rn from cte_dups)
select l.id as input, 'DUP' + cast (cr.rn as varchar(2)) as output from list l 
left join cte_rank cr 
on l.id = cr.id
```
