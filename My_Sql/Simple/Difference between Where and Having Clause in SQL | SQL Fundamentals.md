```SQL
--#Where clause
--Where clause apply the filter row by row (individual rows)

select * from emp where salary > 10000;
--Retrieve the records whose salary is greater than 10000

--#Having clause
--Having clause is used to apply the filter on aggregated function.

select department_id, avg(salary) from emp
group by department_id
having avg(salary) > 9500
--Retrieve those records whose average salary of department_id is greater than 9500

--# Both Where and Having clause
select department_id, avg(salary) from emp
where salary > 10000
group by department_id
having avg(salary) > 12000
-- In this case first filter records whose salary greater than 10000 and then group by
   remaining records based department_id and filter aggregation function

--Note:- From > Where > Group by > Having
```
