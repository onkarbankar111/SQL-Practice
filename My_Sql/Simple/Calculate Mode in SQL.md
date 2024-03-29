Mean - We calculate the mean by using aggregate function (Avg() function)

Mode -  Mode is nothing but the most frequent value in the array

eg -1] 1,2,3,3,4,5,6,6,6     mode = 6 (most frequent value in array)
   
  2]1,2,3,3,3,4,5,6,6,6    mode = 3,6 (This is multimode array. These two values (3 & 6) are equally frequent)

```SQL
create table mode 
(
id int
);
insert into mode values (1),(2),(2),(3),(3),(3),(3),(4),(5);
select * from mode

--Method-1]using cte & subquery
with freq_cte as (
select id, count(id) as freq from mode group by id)
select * from freq_cte where freq = (select max(freq) from freq_cte)

--Multi-mode array (Two or more mode values)
INSERT INTO MODE VALUES (4),(4),(4)
select * from mode
with freq_cte as (
select id, count(id) as freq from mode group by id)
select * from freq_cte where freq = (select max(freq) from freq_cte)
--output :- mode=3,4

--Method-2]using cte & rank function
select * from mode
with freq_cte as (
select id, count(id) as freq from mode group by id)
,rnk_cte as (
select *, rank() over (order by freq desc) as rn from freq_cte)
select * from rnk_cte where rn = 1
```
