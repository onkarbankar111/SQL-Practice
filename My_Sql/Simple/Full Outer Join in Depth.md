```SQL
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
```
