```SQL
create table t1
(
  id1 int 
 );
 insert into t1 values (1),(1),(2),(2),(4),(null)
 select * from t1;
 
 create table t2
(
  id2 int 
 );
 insert into t2 values (1),(1),(1),(3),(2),(2),(null)
 select * from t2;
 
 --Inner join
 select * from t1 
 inner join t2 on t1.id1 = t2.id2
 
 --left join 
  select * from t1 
 left join t2 on t1.id1 = t2.id2
 
  --right join 
  select * from t1 
 right join t2 on t1.id1 = t2.id2
 
  --full outer join 
  select * from t1 
 full outer join t2 on t1.id1 = t2.id2
 
 ```
