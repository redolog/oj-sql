# coalesce 函数
coalesce 返回入参集合中第一个非null的值，因此可以用来做类似ifnull的默认值逻辑。

## 语法
```sql
COALESCE(value1, value2, value3....., valueN);  
```

语义等价于：
```sql
IF (value1!= NULL) THEN  
   result = value1;  
ELSIF (value2 != NULL) THEN  
   result = value2;  
ELSE  
   result = NULL;  
END IF;  
```

## 例子
```sql
select
    user.name,
    ifnull(sum(ride.distance),0) as travelled_distance
from Users user
left join Rides ride
on (user.id=ride.user_id)
group by user.id
order by travelled_distance desc, user.name asc;

select
    user.name,
    coalesce(sum(ride.distance),0) as travelled_distance
from Users user
left join Rides ride
on (user.id=ride.user_id)
group by user.id
order by travelled_distance desc, user.name asc;
```
可以看到在赋默认值逻辑上，与ifnull、if分支判断效果一致。