```SQL
Create table orders
(
    Id int primary key identity,
    Continent nvarchar(50),
    Country nvarchar(50),
    City nvarchar(50),
    amount int
);
Insert into orders values('Asia','India','Bangalore',1000)
Insert into orders values('Asia','India','Chennai',2000)
Insert into orders values('Asia','Japan','Tokyo',4000)
Insert into orders values('Asia','Japan','Hiroshima',5000)
Insert into orders values('Europe','United Kingdom','London',1000)
Insert into orders values('Europe','United Kingdom','Manchester',2000)
Insert into orders values('Europe','France','Paris',4000)
Insert into orders values('Europe','France','Cannes',5000)
;
SELECT * FROM orders

SELECT continent,country, city, sum(amount) as total_amount 
FROM orders
GROUP BY continent,country, city
union all
SELECT continent,null country,null city, sum(amount) as total_amount 
FROM orders
GROUP BY continent
union all
SELECT continent,country,null city, sum(amount) as total_amount 
FROM orders
GROUP BY continent, country
union all
SELECT null continent,null country,null city, sum(amount) as total_amount 
FROM orders


--Rollup 
SELECT continent,country, city, sum(amount) as total_amount 
FROM orders
GROUP BY rollup(continent,country, city)
--rolling up sequentially from left to right (city and continent not accepted)
--combination of rollup continent, continent and country, all columns & All null columns 
--similar ouput like above no of union all query output. 

--Cube 
SELECT continent,country, city, sum(amount) as total_amount 
FROM orders
GROUP BY cube (continent,country, city)
-- Showing all possible combinations 

--Grouping sets 
SELECT continent,country, city, sum(amount) as total_amount 
FROM orders
GROUP BY grouping sets ((continent,country), (city))
--Showing only grouping combinations
```
