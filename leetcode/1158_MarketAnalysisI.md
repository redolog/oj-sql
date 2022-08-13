# 题目

[1158. Market Analysis I](https://leetcode.cn/problems/market-analysis-i/)

这道题中文翻译有问题，建议直接看英文版题干。

# 思路
1. 先筛选订单，并计数，再外部用户表左连；

# solution

## 先筛订单，再连用户
```sql
with id2Cnt as (
    select buyer_id, count(distinct order_id) as orders_in_2019
    from Orders
    where order_date between '2019-01-01' and '2019-12-31'
    group by buyer_id
)

select u.user_id as buyer_id, u.join_date, ifnull(id2Cnt.orders_in_2019,0) as orders_in_2019
from Users u
left join id2Cnt id2Cnt
on (u.user_id = id2Cnt.buyer_id)
```

等价的子查询写法：
```sql
select u.user_id as buyer_id, u.join_date, ifnull(id2Cnt.orders_in_2019,0) as orders_in_2019
from Users u
left join (
    select buyer_id, count(distinct order_id) as orders_in_2019
    from Orders id2Cnt
    where order_date between '2019-01-01' and '2019-12-31'
    group by buyer_id
) id2Cnt
on (u.user_id = id2Cnt.buyer_id)
```

## 直接左连
用户表直接左连订单表可以一次通过。

**注意点：筛选条件、分组条件只能用左表字段，否则结果有误。**
```sql
select u.user_id buyer_id, u.join_date, count(o.buyer_id)  as orders_in_2019
from Users u
left join Orders o
on (u.user_id = o.buyer_id and order_date between '2019-01-01' and '2019-12-31')
group by u.user_id
```

## 在结果集上进行订单子查询
```sql
select 
       user_id buyer_id,
       join_date, 
       (
            select count(distinct order_id) from Orders where buyer_id=user_id and order_date between '2019-01-01' and '2019-12-31'
        ) as orders_in_2019
from Users
group by user_id,join_date
```