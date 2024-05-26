```SQL
CREATE TABLE product
( 
    product_category varchar(255),
    brand varchar(255),
    product_name varchar(255),
    price int
);

INSERT INTO product VALUES
('Phone', 'Apple', 'iPhone 12 Pro Max', 1300),
('Phone', 'Apple', 'iPhone 12 Pro', 1100),
('Phone', 'Apple', 'iPhone 12', 1000),
('Phone', 'Samsung', 'Galaxy Z Fold 3', 1800),
('Phone', 'Samsung', 'Galaxy Z Flip 3', 1000),
('Phone', 'Samsung', 'Galaxy Note 20', 1200),
('Phone', 'Samsung', 'Galaxy S21', 1000),
('Phone', 'OnePlus', 'OnePlus Nord', 300),
('Phone', 'OnePlus', 'OnePlus 9', 800),
('Phone', 'Google', 'Pixel 5', 600),
('Laptop', 'Apple', 'MacBook Pro 13', 2000),
('Laptop', 'Apple', 'MacBook Air', 1200),
('Laptop', 'Microsoft', 'Surface Laptop 4', 2100),
('Laptop', 'Dell', 'XPS 13', 2000),
('Laptop', 'Dell', 'XPS 15', 2300),
('Laptop', 'Dell', 'XPS 17', 2500),
('Earphone', 'Apple', 'AirPods Pro', 280),
('Earphone', 'Samsung', 'Galaxy Buds Pro', 220),
('Earphone', 'Samsung', 'Galaxy Buds Live', 170),
('Earphone', 'Sony', 'WF-1000XM4', 250),
('Headphone', 'Sony', 'WH-1000XM4', 400),
('Headphone', 'Apple', 'AirPods Max', 550),
('Headphone', 'Microsoft', 'Surface Headphones 2', 250),
('Smartwatch', 'Apple', 'Apple Watch Series 6', 1000),
('Smartwatch', 'Apple', 'Apple Watch SE', 400),
('Smartwatch', 'Samsung', 'Galaxy Watch 4', 600),
('Smartwatch', 'OnePlus', 'OnePlus Watch', 220);
select * from product;


-- FIRST_VALUE 
-- Write query to display the most expensive product under each category (corresponding to each record)
select *,
first_value(product_name) over(partition by product_category order by price desc) as most_exp_product
from product;

-- Write query to display the least expensive product under each category (corresponding to each record)
select *,
first_value(product_name) over(partition by product_category order by price desc) as most_exp_product,
last_value(product_name) over(partition by product_category order by price desc) as least_exp_product
from product;
--In this case least_exp_product data showing not correct  

--Frame clause- Frame clause is a subset of partition 
--Frame clause is used very important whenever we are using last_value function
--Frame clause is used to fetch the last value data as we want.
select *,
last_value(product_name) over(partition by product_category order by price desc
                             range BETWEEN unbounded preceding and unbounded following )
as least_exp_product
from product;
--This is expected output. 
--Frame clause is nothing but range BETWEEN unbounded preceding and unbounded following


--rows and range are same but Difference between rows and range will come when their are duplicate records 
select *,
last_value(product_name) over(partition by product_category order by price desc
                             range BETWEEN unbounded preceding and current row ) as least_exp_product
from product
where product_category = 'phone';


select *,
last_value(product_name) over(partition by product_category order by price desc
                             rows BETWEEN unbounded preceding and current row ) as least_exp_product
from product
where product_category = 'phone';


-- Alternate way to write SQL query using Window functions
select *,
first_value(product_name) over w as most_exp_product,
last_value(product_name) over w as least_exp_product    
from product
WHERE product_category ='Phone'
window w as (partition by product_category order by price desc
            range between unbounded preceding and unbounded following);

-- NTH_VALUE 

-- Write query to display the Second most expensive product under each category.
select *,
first_value(product_name) over w as most_exp_product,
last_value(product_name) over w as least_exp_product,
nth_value(product_name, 2) over w as second_most_exp_product
from product
window w as (partition by product_category order by price desc
            range between unbounded preceding and unbounded following);
            
select *,
first_value(product_name) over w as most_exp_product,
last_value(product_name) over w as least_exp_product,
nth_value(product_name, 2) over w as second_most_exp_product
from product
window w as (partition by product_category order by price desc
           -- range between unbounded preceding and unbounded following);
-- In this case this query executed row by row because of range function is not used. 
--In this case we want to find second most exp valuse that means first row of nth valuse showing null in each category.
-- Write query to display the Second most expensive product under each category.
select *,
first_value(product_name) over w as most_exp_product,
last_value(product_name) over w as least_exp_product,
nth_value(product_name, 5) over w as fifth_most_exp_product
from product
window w as (partition by product_category order by price desc
            range between unbounded preceding and unbounded following);
--If fifth value of most exp product is not exist then showing null value of entire product category.

- NTILE
-- Write a query to segregate all the expensive phones, mid range phones and the cheaper phones.
--Step - 1]
SELECT *,
ntile(3) over (ORDER by price DESC) as buckets
FROM product 
WHERE product_category = 'Phone'

--Step-2]
select x.product_name, 
case when x.buckets = 1 then 'Expensive Phones'
     when x.buckets = 2 then 'Mid Range Phones'
     when x.buckets = 3 then 'Cheaper Phones' END as Phone_Category
from (
    select *,
    ntile(3) over (order by price desc) as buckets
    from product
    where product_category = 'Phone') x;

-- CUME_DIST (cumulative distribution) ; 
/*  Formula = Current Row no (or Row No with value same as current row) / Total no of rows */

-- Query to fetch all products which are constituting the first 30% 
-- of the data in products table based on price.
select product_name, cume_dist_percetage
from (
    select *,
    cume_dist() over (order by price desc) as cume_distribution,
    round(cume_dist() over (order by price desc) :: (numeric * 100),2)||'%' as cume_dist_percetage
    from product) x
where x.cume_distribution <= 0.3;
-- In this case if duplicate prices available in rows then 
--consider the cume_distribution value in last duplicate price value row because of using order by price


```
