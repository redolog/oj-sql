# 题目

[262. 行程和用户](https://leetcode.cn/problems/trips-and-users/)

# 思路
1. 使用sum、count计数
2. 使用子查询命中有效用户

# solution

## count if subQuery
count内嵌if，完成对应状态的计数，小数位用round处理。
```sql
with bannes_users as (
    select users_id from Users where banned='Yes'
)

select 
       request_at 'Day',
       round(count(if(status!='completed',status,null))/count(*),2) 'Cancellation Rate'
from Trips
where request_at between "2013-10-01" and "2013-10-03"
  and client_id not in (select users_id from bannes_users)
  and driver_id not in (select users_id from bannes_users)
group by request_at;
```
## sum if subQuery
同样，我们还可以用sum来计数。
```sql
with bannes_users as (
    select users_id from Users where banned='Yes'
)

select 
       request_at 'Day',
       round(sum(if(status!='completed',1,0))/count(*),2) 'Cancellation Rate'
from Trips
where request_at between "2013-10-01" and "2013-10-03"
  and client_id not in (select users_id from bannes_users)
  and driver_id not in (select users_id from bannes_users)
group by request_at;
```