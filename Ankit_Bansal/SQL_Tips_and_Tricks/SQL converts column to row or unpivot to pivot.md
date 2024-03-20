```SQL

-- Sql converts column to row and row to column that means unpivot to pivot and pivot to unpivot.

create table emp_compensation (
emp_id int,
salary_component_type varchar(20),
val int
);
insert into emp_compensation
values (1,'salary',10000),(1,'bonus',5000),(1,'hike_percent',10)
, (2,'salary',15000),(2,'bonus',7000),(2,'hike_percent',8)
, (3,'salary',12000),(3,'bonus',6000),(3,'hike_percent',7);
select * from emp_compensation;  --(Unpivot format)

-- Convert column to row or unpivot to pivot
--Step-1]
select emp_id
,case when salary_component_type = 'salary' then val end as salary
,case when salary_component_type = 'bonus' then val end as bonus
,case when salary_component_type = 'hike_percent' then val end as hike_percent
from emp_compensation
--This is not expected output

--Step-2]
select emp_id
,sum(case when salary_component_type = 'salary' then val end) as salary
,sum(case when salary_component_type = 'bonus' then val end) as bonus
,sum(case when salary_component_type = 'hike_percent' then val end) as hike_percent
from emp_compensation
group by emp_id
--This is expected output

```
