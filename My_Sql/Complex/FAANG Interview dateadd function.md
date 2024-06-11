```SQL
--Write a query to provide the date for nth occurence of sunday in future from given date 
--datepart 
--Sunday-1 
--Monday-2 
--Friday-6 
--Saturday-7 

DECLARE @today_date date
DECLARE @n int 
set @today_date = '2022-01-01'  --Saturday 
set @n = 3
SELECT dateadd(day, 8-datepart(weekday, @today_date), @today_date)


DECLARE @today_date date 
DECLARE @n int 
set @today_date = '2022-01-02'
set @n = 3
SELECT dateadd(week,@n-1,dateadd(day, 8-datepart(weekday, @today_date), @today_date))

---------------------or--------------

DECLARE @today_date date 
DECLARE @n int 
set @today_date = '2022-01-02'
set @n = 3
SELECT dateadd(week,@n,dateadd(day, 0, @today_date))
```
