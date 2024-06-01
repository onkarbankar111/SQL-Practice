Input:-				
name	address	email	floor	resources
A	Bangalore	A@gmail.com	1	CPU
A	Bangalore	A1@gmail.com	1	CPU
A	Bangalore	A2@gmail.com	2	DESKTOP
B	Bangalore	B@gmail.com	2	DESKTOP
B	Bangalore	B1@gmail.com	2	DESKTOP
B	Bangalore	B2@gmail.com	1	MONITOR
![image](https://github.com/onkarbankar111/SQL-Practice/assets/164195447/728078a2-6dd4-4f11-98f4-3c1bfb39fd76)


Output:-			
name	total_visits	most_visited_floor	resources_used
A	3	1	CPU,DESKTOP
B	3	2	DESKTOP,MONITOR
![image](https://github.com/onkarbankar111/SQL-Practice/assets/164195447/f68ca155-d896-43fe-8697-4ce7de24ccda)

```SQL
--Solution
create table entries ( 
name varchar(20),
address varchar(20),
email varchar(20),
floor int,
resources varchar(10));
insert into entries 
values ('A','Bangalore','A@gmail.com',1,'CPU'),('A','Bangalore','A1@gmail.com',1,'CPU'),
('A','Bangalore','A2@gmail.com',2,'DESKTOP')
,('B','Bangalore','B@gmail.com',2,'DESKTOP'),('B','Bangalore','B1@gmail.com',2,'DESKTOP'),
('B','Bangalore','B2@gmail.com',1,'MONITOR')
SELECT * FROM entries

--Step-1]
with floor_visit as (
SELECT name, floor, COUNT(floor) as no_of_floor_visit,
rank() over (partition by name order by COUNT(floor) desc) as rn
FROM entries
GROUP by name, floor) 
SELECT name, floor as most_visited_floor FROM floor_visit WHERE rn=1

--Step-2]
SELECT name, count(floor) as total_visits, 
string_agg(resources, ',') as resources_used
FROM entries 
GROUP by name 

--Step-3]
WITH total_visit as (
SELECT name, count(floor) as total_visits, 
string_agg(resources, ',') as resources_used
FROM entries 
GROUP by name)
,floor_visit as (
SELECT name, floor, COUNT(floor) as no_of_floor_visit,
rank() over (partition by name order by COUNT(floor) desc) as rn
FROM entries
GROUP by name, floor) 
SELECT fv.name, tv.total_visits,fv.no_of_floor_visit as most_visited_floor
,tv.resources_used
FROM floor_visit as fv
inner join total_visit tv
on fv.name = tv.name
where rn=1

--Step-4]
WITH distinct_resources as (SELECT DISTINCT name, resources from entries)
,agg_resources as (SELECT name, string_agg(resources,',')as resources_used 
 FROM distinct_resources GROUP by name )
,total_visit as (
SELECT name, count(floor) as total_visits, 
string_agg(resources, ',') as resources_used
FROM entries 
GROUP by name)
,floor_visit as (
SELECT name, floor, COUNT(floor) as no_of_floor_visit,
rank() over (partition by name order by COUNT(floor) desc) as rn
FROM entries
GROUP by name, floor) 
SELECT fv.name, tv.total_visits,fv.no_of_floor_visit as most_visited_floor
,ar.resources_used
FROM floor_visit as fv
inner join total_visit tv on fv.name = tv.name
inner join agg_resources ar on fv.name = ar.name
where rn=1
```
