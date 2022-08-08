# 题目

[181. 超过经理收入的员工](https://leetcode.cn/problems/employees-earning-more-than-their-managers/)

# 考察点
1. 简单连表

# solution

## join连表

```sql
select e.name as `Employee`
from Employee e
join Employee m
on (e.managerId=m.id)
where e.salary > m.salary;
```