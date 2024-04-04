* Running sum in SQL:-

Input table:-
Products:-	
product_id	cost
P1	200
P2	300
P3	300
P4	500
P5	800
	
![image](https://github.com/onkarbankar111/SQL-Practice/assets/164195447/4a082864-6d3b-42c5-8a46-68c40191691e)

Expected Output:-		
product_id	cost	running_cost
P1	200	200
P2	300	500
P3	300	800
P4	500	1300
P5	800	2100
![image](https://github.com/onkarbankar111/SQL-Practice/assets/164195447/009d2eae-8621-4ae4-87b5-70c6d672230f)

Solution:-
```SQL
create table products(
  product_id varchar(2),
  cost int
  )
insert into products values ('P1',200),
('P2',300),('P3',300),('P4',500),('P5',800)
SELECT * FROM products
```

```SQL
select *, sum(cost) over (order by cost asc ) as running_cost from products
```
Output:-		
product_id	cost	running_cost
P1	200	200
P2	300	300
P3	300	300
P4	500	1300
P5	800	2100
![image](https://github.com/onkarbankar111/SQL-Practice/assets/164195447/877f00de-af44-4a7e-88e3-8a0d9c937d36)

--This is not expected output


--There are two methods to find running cost

Method-1]
```SQL
select *, sum(cost) over (order by cost asc, product_id ) as running_cost from products
--This is expected output
```

Method-2]
```SQL
select *, sum(cost) over (order by cost asc rows BETWEEN unbounded preceding and current row ) 
as running_cost from products
--This is expected output
```
