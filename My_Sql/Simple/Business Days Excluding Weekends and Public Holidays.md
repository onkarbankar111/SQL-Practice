```SQL
create table tickets
(
ticket_id varchar(10),
create_date date,
resolved_date date
);

insert into tickets values
(1,'2022-08-01','2022-08-03')
,(2,'2022-08-01','2022-08-12')
,(3,'2022-08-01','2022-08-16');

SELECT * from tickets
--Find out the buisness days excluding weekends only
SELECT *,
datediff(day, create_date, resolved_date) as actual_days,
datepart(week, create_date) as week_no_of_create_date,
datepart(week, resolved_date) as week_no_of_resolved_date,
datediff(week, create_date, resolved_date) as week_diff,
datediff(day, create_date, resolved_date) -2*datediff(week, create_date, resolved_date) as buisness_days
from tickets


create table holidays
(
holiday_date date
,reason varchar(100)
);
insert into holidays values
('2022-08-11','Rakhi'),('2022-08-15','Independence day');
SELECT * FROM holidays

--Find out the buisness days excluding weekends and public holidays 
--Step-1]
select * from tickets 
left join holidays 
on holiday_date BETWEEN create_date and resolved_date

--step-2] Find the number of holidays 
select ticket_id, create_date, resolved_date, COUNT(holiday_date) no_of_holidays from tickets 
left join holidays 
on holiday_date BETWEEN create_date and resolved_date
GROUP BY ticket_id, create_date, resolved_date  

--Step-3]Find out the buisness days excluding weekends and public holidays
select *, 
datediff(day, create_date, resolved_date) -2*datediff(week, create_date, resolved_date)-no_of_holidays
as buisness_days
from (
select ticket_id, create_date, resolved_date, COUNT(holiday_date) no_of_holidays from tickets 
left join holidays 
on holiday_date BETWEEN create_date and resolved_date
GROUP BY ticket_id, create_date, resolved_date) as a 
--        OR 
with cte as(
select ticket_id, create_date, resolved_date, COUNT(holiday_date) no_of_holidays from tickets 
left join holidays 
on holiday_date BETWEEN create_date and resolved_date
GROUP BY ticket_id, create_date, resolved_date)
SELECT *, datediff(day, create_date, resolved_date) -2*datediff(week, create_date, resolved_date)-no_of_holidays
as buisness_days from cte
```
