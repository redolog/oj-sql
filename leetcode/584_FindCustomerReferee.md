# 题目

[584. 寻找用户推荐人](https://leetcode.cn/problems/find-customer-referee/)

# 思路
1. 直接条件筛，先查refereeId为null的，再查refereeId有值且不为2的，当然，可以写两条select进行union；
2. 使用notin进行反筛，每条数据都有id，使用id notin (refereeId为2的id)；

# solution

## 先null再!=2
```sql
select
    name
from
    Customer
where referee_id is null or referee_id!=2;
```
## notin
```sql
select
    name
from
    Customer
where id not in (select id from Customer where referee_id=2);
```