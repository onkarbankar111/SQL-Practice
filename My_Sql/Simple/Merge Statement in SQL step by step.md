```Sql
CREATE TABLE SourceProducts(
    ProductID  INT,
    ProductName  VARCHAR(50),
    Price INT
);
INSERT INTO SourceProducts VALUES(1,'Table',90),(3,'Chair',70) 
SELECT * FROM SourceProducts

CREATE TABLE TargetProducts(
    ProductID  INT,
    ProductName  VARCHAR(50),
    Price INT
);
INSERT INTO TargetProducts VALUES(1,'Table',100),(2,'Desk',180)
SELECT * FROM TargetProducts

--We want to merge SourceProducts table into TargetProducts table 
SELECT * FROM SourceProducts
SELECT * FROM TargetProducts

--Solution:-
-- Steps- updated matched productID and  inserted unmatched productid into TargetProducts table 

--Step-1] 
merge TargetProducts t 
using SourceProducts s 
on t.ProductID = s.ProductID 
when matched then update 
set t.Price = s.Price, t.ProductName = s.ProductName;

SELECT * FROM TargetProducts
-- update the matched productid
--Semicolon is mandatory for teminate the merge statement. otherwise showing error

--Step-2] 
merge TargetProducts t 
using SourceProducts s 
on t.ProductID = s.ProductID 
when matched then update 
set t.Price = s.Price, t.ProductName = s.ProductName
when not matched by target then 
INSERT VALUES (s.ProductID, s.ProductName, s.Price);

SELECT * FROM TargetProducts
--Insert unmatched records into TargetProducts as well
```
