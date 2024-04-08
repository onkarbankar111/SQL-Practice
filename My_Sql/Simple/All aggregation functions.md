*Aggregation functions :- sum(), avg(), min(), max()

Practicals:-

Input table:-	(int_orders)		
salesperson_is	order_number	order_date	amount
1	30	14/07/1995	460
2	10	2/1/1996	540
2	40	29/01/1998	2400
7	50	3/2/1998	600
7	60	2/3/1998	720
7	70	6/5/1998	150
8	20	30/01/1999	180
![image](https://github.com/onkarbankar111/SQL-Practice/assets/164195447/c17927f9-b279-47bf-94aa-3a953be4bd8a)

Solutions :-

```SQL
create table int_orders(
  salesperson_id int,
  order_number int,
  order_date varchar(20),
  amount int
  )
insert into int_orders values (1,30,'1995-07-14',460),
(2,10,'1996-08-02',540),(2,40,'1998-01-29',2400),(7,50,'1998-02-03',600),
(7,60,'1998-03-02',720),(7,70,'1998-05-06',150),(8,20,'1999-01-30',1800)
select * from int_orders

select sum(amount) from int_orders

select salesperson_id, sum(amount) from int_orders
group by salesperson_id

select salesperson_id,order_number, sum(amount) from int_orders
group by salesperson_id
--showing error

select salesperson_id,order_number, sum(amount) from int_orders
group by salesperson_id, order_number

select salesperson_id, order_number,order_date, amount, 
sum(amount) over() from int_orders

select salesperson_id, order_number,order_date, amount, 
sum(amount) over(Partition by salesperson_id) from int_orders

select salesperson_id, order_number,order_date, amount, 
sum(amount) over(order by order_date) from int_orders

select salesperson_id, order_number,order_date, amount, 
sum(amount) over(partition by salesperson_id order by order_date) 
from int_orders

select salesperson_id, order_number,order_date, amount, 
sum(amount) over(order by order_date rows between 2 preceding and current row) 
from int_orders

select salesperson_id, order_number,order_date, amount, 
sum(amount) over(order by order_date rows between 2 preceding and 1 preceding) 
from int_orders

select salesperson_id, order_number,order_date, amount, 
sum(amount) over(order by order_date rows between 1 preceding and 1 preceding) 
from int_orders

select salesperson_id, order_number,order_date, amount, 
sum(amount) over(order by order_date rows between 1 preceding and 1 following) 
from int_orders

select salesperson_id, order_number,order_date, amount, 
sum(amount) over(order by order_date rows between unbounded preceding and current row) 
from int_orders
--Unbounded preceding means all the previous rows

select salesperson_id, order_number,order_date, amount, 
sum(amount) over(partition by salesperson_id order by order_date rows between 1 preceding and current row) 
from int_orders

select salesperson_id, order_number,order_date, amount, 
sum(amount) over(order by order_date rows between 2 preceding and 1 preceding) 
from int_orders

select salesperson_id, order_number,order_date, amount, 
sum(amount) over(order by order_date rows between 1 following and 1 following) 
from int_orders
```
