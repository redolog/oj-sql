# 题目

[1141. 查询近30天活跃用户数](https://leetcode.cn/problems/user-activity-for-the-past-30-days-i/)

# 思路
1. 先筛选，再分组，再计数；

# solution

## where groupby count
```sql
select activity_date as day, count(distinct user_id) as active_users
from Activity
where activity_date between '2019-06-28' and '2019-07-27'
group by activity_date
;
```