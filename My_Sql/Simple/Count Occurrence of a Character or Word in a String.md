```SQL
create table strings (
  name varchar(50)
)
insert into strings values ('Ankit Bansal'),
('Ram Kumar Verma'),('Akshay Kumar Ak k'),('Rahul')
select * from strings

select name, replace(name,' ','') as rep_name from strings
--Space is replace with empty value.

select name, replace(name,' ','') as rep_name,
len(name) - len(replace(name,' ','')) as cnt
from strings
--Count the number of spaces.

select name, replace(name,'Ak','') as rep_name,
len(name) - len(replace(name,'Ak','')) as character, 
(len(name) - len(replace(name,'Ak','')))/len('Ak') as Occurence
from strings
--Note:- Occurence of Ak is 2 means character = occurence(no of words) * no of character in words=2*2=4
```
