* Update statement :-

  Update and Alter both are different things

Update- Update statement is used to update the data(Updating the row). Update statement cannot
used to update column structure or table structure.

Alter :- Alter statement is used to update the column structure or table structure.
i.g we want to add or delete the column, we want to update the datatype of column


1- Update basic syntax
update emp set salary = 12000
--In this case update the salary column value for all rows

2- Update with where clause
update emp set salary = 12000 where emp_id = 1
update emp set salary = 12000 where emp_age >30
--In this case update the salary value only for which satisfies the where condition.

3- Update multiple values 
update emp set salary = 12000 , dep_id = 200 where emp_id=2
--In this case update the multiple values only for which satisfies the where condition.

4- Update using calculations (Col calculation / case when)
update emp set salary =salary + 1000
--In this case update the salary column for each rows having salary + 1000
update emp set salary = salary * 1.1 where emp_id=4
--In this case increase the salary of 10 % who has emp_id 4
update emp set salary = case when dep_id = 100 then salary * 1.1
                             when dep_id = 200 then salary * 1.2
                             else salary
                        end

5- Update using Join


6- Interview question on Update
7- Some tips and tricks on sql update
