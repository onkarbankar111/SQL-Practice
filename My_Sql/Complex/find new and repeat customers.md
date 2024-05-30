Input:-			
order_id	customer_id	order_date	order_amount
1	100	1/1/2022	2000
2	200	1/1/2022	2500
3	300	1/1/2022	2100
4	100	2/1/2022	2000
5	400	2/1/2022	2200
6	500	2/1/2022	2700
7	100	3/1/2022	3000
8	400	3/1/2022	1000
9	600	3/1/2022	3000
![image](https://github.com/onkarbankar111/SQL-Practice/assets/164195447/06f53039-bed4-4e6d-8b9c-de4e04ce1b10)

Output:-		
ordar_date	no_of_new_customers	no_of_repeat_customers
1/1/2022	3	0
2/1/2022	2	1
3/1/2022	1	2
![image](https://github.com/onkarbankar111/SQL-Practice/assets/164195447/7963e505-d7ec-4af4-b501-44e343ce2650)

```SQL
create table customer_orders (
order_id integer,
customer_id integer,
order_date date,
order_amount integer
);
insert into customer_orders values(1,100,cast('2022-01-01' as date),2000),
(2,200,cast('2022-01-01' as date),2500),(3,300,cast('2022-01-01' as date),2100)
,(4,100,cast('2022-01-02' as date),2000),(5,400,cast('2022-01-02' as date),2200),
(6,500,cast('2022-01-02' as date),2700),(7,100,cast('2022-01-03' as date),3000),
(8,400,cast('2022-01-03' as date),1000),(9,600,cast('2022-01-03' as date),3000)
select * from customer_orders

--Solution]
--step-1]
SELECT customer_id, min(order_date) as first_visit_date 
FROM customer_orders
GROUP BY customer_id
--Step-2]
with first_visit as (
SELECT customer_id, min(order_date) as first_visit_date 
FROM customer_orders
GROUP BY customer_id ) 
SELECT co.*, fv.first_visit_date
FROM customer_orders co
inner JOIN first_visit fv 
on co.customer_id = fv.customer_id
order by order_id 
--step-3]
with first_visit as (
SELECT customer_id, min(order_date) as first_visit_date 
FROM customer_orders
GROUP BY customer_id ),
visit_flag as (
SELECT co.*, fv.first_visit_date ,
case when co.order_date = fv.first_visit_date then 1 else 0 end as first_visit_flag,
case when co.order_date != fv.first_visit_date then 1 else 0 end as repeat_visit_flag
FROM customer_orders co
inner JOIN first_visit fv 
on co.customer_id = fv.customer_id)
SELECT order_date, sum(first_visit_flag) as no_of_new_customers, 
sum(repeat_visit_flag) as no_of_repeat_customers
FROM visit_flag
GROUP BY order_date;
```
