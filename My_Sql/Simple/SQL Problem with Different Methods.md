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
```
