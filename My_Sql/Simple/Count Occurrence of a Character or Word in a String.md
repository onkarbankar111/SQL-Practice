```SQL
create table strings (
  name varchar(50)
)
insert into strings values ('Ankit Bansal'),
('Ram Kumar Verma'),('Akshay Kumar Ak k'),('Rahul')
select * from strings

select name, replace(name,' ','') as rep_name from strings

select name, replace(name,' ','') as rep_name,
len(name) - len(replace(name,' ','')) as cnt
from strings

select name, replace(name,'Ak','') as rep_name,
len(name) - len(replace(name,'Ak','')) as cnt
from strings

select name, replace(name,'Ak','') as rep_name,
(len(name) - len(replace(name,'Ak','')))/len('Ak') as cnt
from strings
```
