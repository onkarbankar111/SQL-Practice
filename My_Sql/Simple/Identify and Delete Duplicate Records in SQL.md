```SQL
-- Find duplicates 
SELECT emp_id, count(1) from employee 
GROUP BY emp_id 
having count(1)>1

--Delete duplicates 
DELETE FROM employee WHERE (emp_id, salary) in (SELECT emp_id, min(salary) as salary
                                                         from employee group by emp_id HAVING count(1)>1)
```
