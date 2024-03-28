Cross Join - Cross join is nothing but cartesian product.
eg - There are two table A & B. 5 records in table A & 3 Records in table B
then the output of cross join A & B shows 15 records. i.g 5*3=15

```SQL
create table products (
id int,
name varchar(10)
);
insert into products VALUES 
(1, 'A'),(2, 'B'),(3, 'C'),
(4, 'D'),(5, 'E');
select * from products

create table colors (
color_id int,
color varchar(50)
);
insert into colors values (1,'Blue'),(2,'Green'),(3,'Orange');
select * from colors

create table sizes
(
size_id int,
size varchar(10)
);
insert into sizes values (1,'M'),(2,'L'),(3,'XL');
select * from sizes

create table transactions
(
order_id int,
product_name varchar(20),
color varchar(10),
size varchar(10),
amount int
);
insert into transactions values (1,'A','Blue','L',300),
(2,'B','Blue','XL',150),(3,'B','Green','L',250),(4,'C','Blue','L',250),
(5,'E','Green','L',270),(6,'D','Orange','L',200),(7,'D','Green','M',250);
select * from transactions

--Cross join of products and sizes table
select p.*, s.* from products p, sizes s

select product_name, color, size, sum(amount) as total_amount
from transactions
group by product_name, color, size

--Cross join of products, colors and sizes table
select p.*,c.*, s.* from products p,colors c, sizes s

--Find out the total amount of each combination(product_name, color, size) of product sale
with master_data as (
select p.name as product_name, c.color, s.size from products p, colors c, sizes s)
, sales as (
select product_name, color, size, sum(amount) as total_amount
from transactions
group by product_name, color, size )
select md.product_name, md.color, md.size, isnull (s.total_amount,0) as total_amount
from master_data md
left join sales s on md.product_name = s.product_name 
and md.color=s.color and md.size = s.size
order by total_amount
```
