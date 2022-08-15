# 题目

[1741. Find Total Time Spent by Each Employee](https://leetcode.cn/problems/find-total-time-spent-by-each-employee/)

# 思路
1. group by 
2. sum

# solution

## group by sum 
```sql
select
    event_day as day,
    emp_id,
    sum(out_time-in_time) as total_time
from Employees
group by event_day,emp_id;
```