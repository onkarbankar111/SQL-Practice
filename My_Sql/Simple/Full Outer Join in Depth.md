```SQL
--Type-1]
create table orders_usa
(
order_id int,
product_id int,
sales int
);
INSERT INTO orders_usa values (1,100,500)
SELECT * FROM orders_usa

create table orders_europe
(
order_id int,
product_id int,
sales int
);
INSERT INTO orders_europe values (2,200,500)
SELECT * FROM orders_europe

create table orders_india
(
order_id int,
product_id int,
sales int
);
INSERT INTO orders_india values (3,100,500),(4,200,600)
SELECT * FROM orders_india


--Expected output 
--   product_id   sales_usa     sales_europe     sales_india 
--      100         500           null             500
--      200         null          500              600 

--Solution]  
--Step-1]
select coalesce(u.product_id, e.product_id) as product_id,u.sales as sales_usa, e.sales as sales_europe 
from orders_usa u
full outer join orders_europe e
on u.product_id = e.product_id

--Step-2]
select coalesce(u.product_id, e.product_id, i.product_id) as product_id
,u.sales as sales_usa, e.sales as sales_europe, i.sales as sales_india
from orders_usa u
full outer join orders_europe e 
on u.product_id = e.product_id
full outer join orders_india i
on coalesce(u.product_id, e.product_id) = i.product_id

--Type-2]
create table orders_usa
(
order_id int,
product_id int,
sales int
);
insert into orders_usa values (1,100,500);
insert into orders_usa values (7,100,500);
SELECT * FROM orders_usa

create table orders_europe
(
order_id int,
product_id int,
sales int
);
INSERT INTO orders_europe values (2,200,600)
SELECT * FROM orders_europe

create table orders_india
(
order_id int,
product_id int,
sales int
);
insert into orders_india values (3,100,500);
insert into orders_india values (4,200,600);
insert into orders_india values (8,100,500);
SELECT * FROM orders_india


--Expected output 
--   product_id   sales_usa     sales_europe     sales_india 
--      100         1000          null            1000
--      200         null          600              600 

--Solution] 
--Step-1] 
select coalesce(u.product_id, e.product_id, i.product_id) as product_id
,u.sales as sales_usa, e.sales as sales_europe, i.sales as sales_india
from orders_usa u
full outer join orders_europe e 
on u.product_id = e.product_id
full outer join orders_india i
on coalesce(u.product_id, e.product_id) = i.product_id

--Step-2]
select coalesce(u.product_id, e.product_id, i.product_id) as product_id
,u.sales as sales_usa, e.sales as sales_europe, i.sales as sales_india
from (SELECT product_id, sum(sales) as sales from orders_usa GROUP BY product_id) u
full outer join (SELECT product_id, sum(sales) as sales from orders_europe GROUP BY product_id) e 
on u.product_id = e.product_id
full outer join (SELECT product_id, sum(sales) as sales from orders_india GROUP BY product_id) i
on coalesce(u.product_id, e.product_id) = i.product_id
order by product_id 
```
