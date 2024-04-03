```SQL
create table happiness_index (
  Rank int,
  Country varchar(20),
  Happiness_2023 float
 )
 insert into happiness_index values (1,'Finland',7.842),
 (2,'Denmark',7.62),(3,'Switzerland',7.571),(4,'India',3.819),
 (5,'Pakistan',4.934),(6,'Iceland',7.554),(7,'Sri Lanka',4.325),
 (8,'Norway',7.392)
 select * from happiness_index
 
 --Sorting Happiness Index Data with India on Top
 select *, case when country = 'India' then 1 else 0 end as country_derivd 
 from happiness_index order by country_derivd desc, Happiness_2023 desc
 
--Sorting Happiness Index Data with India on Top, Pakistan second top and Sri Lanka third top
--Method-1]
  select *,country_derivd = case 
  when country = 'India' then 3 
  when country = 'Pakistan' then 2
  when country = 'Sri Lanka' then 1
  else 0 end 
 from happiness_index order by country_derivd desc, Happiness_2023 desc
 
 --Method-2]
 select * from happiness_index
 order by case 
  when country = 'India' then 3 
  when country = 'Pakistan' then 2
  when country = 'Sri Lanka' then 1
  else 0 end desc , Happiness_2023 desc
```
