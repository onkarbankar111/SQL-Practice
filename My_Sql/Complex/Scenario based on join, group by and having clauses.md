Input:-		
PersonID	Name	Score
1	Alice	86
2	Bob	11
3	Davis	27
4	Tara	45
5	John	63

![image](https://github.com/onkarbankar111/SQL-Practice/assets/164195447/72364453-d068-406e-83bb-4cd795d5ba5e)

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

```SQL
--Solution]
CREATE table person(
  PersonID int,
  name varchar(20),
  Score int
  )
INSERT into person VALUES (1,'Alice',86), 
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

```
