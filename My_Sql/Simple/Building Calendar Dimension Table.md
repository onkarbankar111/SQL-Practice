```SQL
SELECT cast('2000-01-01' as date) as cal_date,
datepart(year,'2000-01-01') as cal_year,
datepart(dayofyear,'2000-01-01') as cal_year_day,
datepart(quarter,'2000-01-01') as cal_quarter,
datepart(month,'2000-01-01') as cal_month,
datename(month,'2000-01-01') as cal_month_name,
datepart(day,'2000-01-01') as cal_month_day,
datepart(week,'2000-01-01') as cal_week,
datepart(weekday,'2000-01-01') as cal_weekday,
datename(weekday,'2000-01-01') as cal_day_name


-- Recursive cte 
--Basic logic
with cte as (
SELECT 1 as id 
UNION all
SELECT id + 1 as id 
from cte 
where id < 10 
)
SELECT * FROM cte


with cte as (
SELECT 1 as id 
UNION all
SELECT id + 1 as id 
from cte 
where id < 200 
)
SELECT * FROM cte
--showing error

--*Maximum recursion 100 has been exhausted before statement completion.Bydefault Maximum recursion limit is 100

with cte as (
SELECT 1 as id 
UNION all
SELECT id + 1 as id 
from cte 
where id < 200 
)
SELECT * FROM cte 
option(MAXRECURSION 300)
--In this case recursion limit is extended. We can increase recursion limit.

--Solution
with cte as (
SELECT cast('2000-01-01' as date) as cal_date,
datepart(year,'2000-01-01') as cal_year,
datepart(dayofyear,'2000-01-01') as cal_year_day,
datepart(quarter,'2000-01-01') as cal_quarter,
datepart(month,'2000-01-01') as cal_month,
datename(month,'2000-01-01') as cal_month_name,
datepart(day,'2000-01-01') as cal_month_day,
datepart(week,'2000-01-01') as cal_week,
datepart(weekday,'2000-01-01') as cal_weekday,
datename(weekday,'2000-01-01') as cal_day_name
UNION all
SELECT dateadd(day,1,cal_date) as cal_date,
datepart(year, dateadd(day,1,cal_date)) as cal_year,
datepart(dayofyear, dateadd(day,1,cal_date)) as cal_year_day,
datepart(quarter, dateadd(day,1,cal_date)) as cal_quarter,
datepart(month, dateadd(day,1,cal_date)) as cal_month,
datename(month, dateadd(day,1,cal_date)) as cal_month_name,
datepart(day, dateadd(day,1,cal_date)) as cal_month_day,
datepart(week, dateadd(day,1,cal_date)) as cal_week,
datepart(weekday, dateadd(day,1,cal_date)) as cal_weekday,
datename(weekday, dateadd(day,1,cal_date)) as cal_day_name

from cte 
where cal_date < cast('2030-12-31' as date)
)
SELECT row_number() over (order by cal_date asc) as rn, * FROM cte 
option(MAXRECURSION 30000)

--In MS SQL maximum extenedable limit is 10000

```
