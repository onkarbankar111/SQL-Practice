```SQL
create table students  (
student_id int,
skill varchar(20)
);
insert into students values
(1,'sql'),(1,'python'),(1,'tableau'),(2,'sql'),(3,'sql'),(3,'python')
,(4,'tableau'),(5,'python'),(5,'tableau');
SELECT * FROM students

--Find the students who knows only sql and python

--Solution:-
--Method-1] Using cte
with cte as (
SELECT student_id, COUNT(*) as total_skill,
count(case when skill in ('sql','python') then skill else null end) as sp_skill
FROM students
GROUP by student_id) 
SELECT * FROM cte where total_skill=2 and sp_skill=2

--Method-2]Using having clause
SELECT student_id, COUNT(*) as total_skill,
count(case when skill in ('sql','python') then skill else null end) as sp_skill
FROM students
GROUP by student_id
HAVING COUNT(*) =2 and count(case when skill in ('sql','python') then skill else null end) =2

--Method-3]
SELECT student_id, COUNT(*) as total_skill,
count(case when skill not in ('sql','python') then skill else null end) as spn_skill
FROM students
GROUP by student_id
HAVING COUNT(*) =2 and count(case when skill not in ('sql','python') then skill else null end) = 0

--Method-4]
SELECT student_id, COUNT(*) as total_skill
FROM students
WHERE student_id not in (SELECT student_id FROM students WHERE skill not in ('sql','python'))
GROUP by student_id
HAVING COUNT(*) = 2

--Method-5] Using except 
SELECT student_id
FROM students
GROUP by student_id
HAVING COUNT(*) = 2
except
SELECT student_id FROM students 
WHERE skill not in ('sql','python')

--Method-6]
with sql as (SELECT * FROM students where skill = 'sql')
, python as (SELECT * FROM students where skill = 'python')
, other AS (SELECT * FROM students where skill NOT IN ('sql','python'))
SELECT s.*, p.*, o.*
from sql s 
inner join python p 
on s.student_id = p.student_id
left join other o
on o.student_id = s.student_id
WHERE o.student_id is null
```
