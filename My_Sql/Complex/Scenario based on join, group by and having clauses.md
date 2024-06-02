Input:-		
PersonID	Name	Score
1	Alice	88
2	Bob	11
3	Davis	27
4	Tara	45
5	John	63

![image](https://github.com/onkarbankar111/SQL-Practice/assets/164195447/8f1393d6-5742-4624-a496-bafd567bd4b7)

Input:-	
PersonID	FriendID
1	2
1	3
2	1
2	3
3	5
4	2
4	3
4	5

![image](https://github.com/onkarbankar111/SQL-Practice/assets/164195447/ff8f9637-5409-4d88-b10b-1d05ba71a37f)

Output:-			
person_id	name	no_of_friends	total_friend_score
2	Bob	2	115
4	Tara	3	101

![image](https://github.com/onkarbankar111/SQL-Practice/assets/164195447/2616040c-6e93-4204-8456-cee57243b6e9)

--Write a query to find person_id, name, no_of_friends, sum of marks of person
who have friends with total score greater than 100

```SQL
--Solution]
CREATE table person(
  PersonID int,
  name varchar(20),
  Score int
  )
INSERT into person VALUES (1,'Alice',88), 
  (2,'Bob',11),(3,'Davis',27), 
  (4,'Tara',45),( 5,'John',63)
CREATE table friend (
  PersonID int,
  FriendID int
)
INSERT into friend values (1,2),(1,3),(2,1),(2,3),
(3,5),(4,2),(4,3),(4,5)
SELECT * FROM person
SELECT * FROM friend

--Step-1]
SELECT f.PersonID, f.FriendID, p.Score as friend_score
from friend f 
inner join person p 
on f.FriendID = p.PersonID

--Step-2]
SELECT f.PersonID, sum(p.Score) as total_friend_score
from friend f 
inner join person p 
on f.FriendID = p.PersonID
GROUP by f.PersonID

--Step-3]
SELECT f.PersonID, sum(p.Score) as total_friend_score
from friend f 
inner join person p 
on f.FriendID = p.PersonID
GROUP by f.PersonID
HAVING sum(p.Score) > 100

--Step-4]
SELECT f.PersonID, sum(p.Score) as total_friend_score,
COUNT(f.FriendID) as no_of_friends
from friend f 
inner join person p 
on f.FriendID = p.PersonID
GROUP by f.PersonID
HAVING sum(p.Score) > 100

--Step-5]
with score_details as (
SELECT f.PersonID, sum(p.Score) as total_friend_score,
COUNT(f.FriendID) as no_of_friends
from friend f 
inner join person p 
on f.FriendID = p.PersonID
GROUP by f.PersonID
HAVING sum(p.Score) > 100
)
SELECT s.*, p.Name as Name
from score_details s 
inner join person p 
on s.PersonID = P.PersonID

```
