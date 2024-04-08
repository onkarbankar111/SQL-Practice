```SQL
CREATE table customers(
  customer_id int,
  customer_name varchar(15),
  gender char,
  dob varchar(10),
  age int 
  )
INSERT into customers values (1,'Rahul','M','2000-01-05',22),
(2,'Shilpa','F','2004-01-05',18),(3,'Ramesh','M','2003-07-07',19),
(4,'Katrina','F','2005-02-05',17),(5,'Alka','F','1992-01-01',30)
select * from customers

create table customer_orders(
  order_id int,
  customer_id int,
  order_date varchar(20),
  ship_date varchar(20)
)
insert into customer_orders values (1000,1,'2022-01-05','2022-01-11'),
(1001,2,'2022-02-04','2022-02-16'),(1002,3,'2022-01-01','2022-01-19'),
(1003,4,'2022-01-06','2022-01-30'),(1004,6,'2022-02-07','2022-02-13')
SELECT * from customer_orders

--Full outer join Method

select c.customer_id, c.customer_name, co.customer_id as co_customer_id, co.order_date
FROM customers c 
full outer join customer_orders co 
on c.customer_id = co.customer_id

--union all Method 
select c.customer_id, c.customer_name, co.customer_id as co_customer_id, co.order_date
FROM customers c 
left join customer_orders co 
on c.customer_id = co.customer_id
union all
select c.customer_id, c.customer_name, co.customer_id as co_customer_id, co.order_date
FROM customers c 
right join customer_orders co 
on c.customer_id = co.customer_id
where c.customer_id is null

--Using union Method
select c.customer_id, c.customer_name, co.customer_id as co_customer_id, co.order_date
FROM customers c 
left join customer_orders co 
on c.customer_id = co.customer_id
union
select c.customer_id, c.customer_name, co.customer_id as co_customer_id, co.order_date
FROM customers c 
right join customer_orders co 
on c.customer_id = co.customer_id
```
