```SQL
-- Find duplicates 
SELECT emp_id, count(1) from employee 
GROUP BY emp_id 
having count(1)>1

--Delete duplicates 
DELETE FROM employee WHERE (emp_id, salary) in (SELECT emp_id, min(salary) as salary
                                                         from employee group by emp_id HAVING count(1)>1)
                                                         
--Find pure Duplicates 
SELECT DISTINCT * from employee


SELECT emp_id, emp_name, salary FROM (
SELECT *, row_number() over (partition by emp_id order by salary)as rn from employee) a 
where rn=1

SELECT emp_id, emp_name, salary FROM (
SELECT *, row_number() over (partition by emp_id order by create_timestamp)as rn from employee) a 
where rn=1
```
