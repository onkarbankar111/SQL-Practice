Input:-		
Team_1	Team_2	Winner
India	SL	India
SL	Aus	Aus
SA	Eng	Eng
Eng	NZ	NZ
Aus	India	India
![image](https://github.com/onkarbankar111/SQL-Practice/assets/164195447/a054ab35-99bf-4f32-a606-0349c587c091)

Output:-			
Team_Name	Matches_played	no_of_wins	no_of_losses
India	2	2	0
SL	2	0	2
SA	1	0	1
Eng	2	1	1
Aus	2	1	1
NZ	1	1	0

![image](https://github.com/onkarbankar111/SQL-Practice/assets/164195447/5b22b1c4-cabb-40ee-8225-0889ec26e9b7)

```SQL
--Solution] 
with cte as (
SELECT Team_1 as Team_Name, case when Team_1 = Winner then 1 else 0 end as win_flag 
FROM icc_world_cup
UNION all 
SELECT Team_2 as Team_Name, case when Team_2 = Winner then 1 else 0 end as win_flag 
FROM icc_world_cup
)
SELECT Team_Name, COUNT(Team_Name) as Matches_played, sum(win_flag) as no_of_wins,
COUNT(Team_Name)-sum(win_flag) as no_of_losses
FROM cte
group by Team_Name
```
