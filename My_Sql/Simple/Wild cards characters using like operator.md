Wild cards characters:- % and _ both are the wild card characters.   
Wild cards characters are used with the Like Operator and not like operator

'%' - 0 OR More characters       
'_' - only one character or single character    
'[]' - anything within bracket can come

Practicals:-
```SQL
--Pattern matching using wildcard character (Like operator)

select order_id, order_date, customer_name from orders
where customer_name = 'Andrew Allen'
--filter the records whose customer_name Andrew Allen
 
select order_id, order_date, customer_name from orders
where customer_name LIKE 'Andrew%'
--filter the records whose customer_name starts with Andrew and after Andrew 0 or more characters 

select order_id, order_date, customer_name from orders
where customer_name LIKE '%Allen'
--filter the records whose customer_name end with Allen and before Allen 0 or more characters 

select order_id, order_date, customer_name from orders
where customer_name LIKE 'A%n'
--filter the records whose customer_name starting with A and ending with n 

select order_id, order_date, customer_name from orders
where customer_name LIKE '%All%'
--Before and after All 0 or more than 0 characters 

select order_id, order_date, customer_name from orders
where customer_name LIKE '_a%'
--filter the customer_name whose name of second character is a

select order_id, order_date, customer_name from orders
where customer_name LIKE '__a%'
--filter the customer_name whose name of third character is a

select order_id, order_date, customer_name from orders
where customer_name LIKE 'A[ns]%'
--Filter the records whose customer name starting with character A and 
--second character is n or s and then 0 or more than 0 character

select order_id, order_date, customer_name from orders
where customer_name LIKE 'A[^ns]%'
--Filter the records whose customer name starting with character A and 
--second character is neither n nor s and then 0 or more than 0 character

select order_id, order_date, customer_name from orders
where customer_name LIKE 'A[b-k]%'
--Filter the records whose customer name starting with character A and 
--second character is between b and k and then 0 or more than 0 character

select order_id, order_date, customer_name from orders
where customer_name NOT LIKE 'A[b-k]%'
```
