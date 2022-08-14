# 题目

[1407. Top Travellers](https://leetcode.cn/problems/top-travellers/)

# 思路
1. 左连表，根据userId分组，根据统计distance排序，null值使用ifnull、coalesce函数处理默认值。

# solution

## groupby if sum
```sql
with distanceReport as (
    select user_id,sum(distance) distance
    from Rides
    group by user_id
)

select user.name , ifnull(ride.distance,0) as travelled_distance
from Users user
left join distanceReport ride
on (user.id=ride.user_id)
order by ride.distance desc, user.name asc

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