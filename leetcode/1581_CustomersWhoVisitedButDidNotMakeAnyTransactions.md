# 题目

[1581. Customer Who Visited but Did Not Make Any Transactions](https://leetcode.cn/problems/customer-who-visited-but-did-not-make-any-transactions/)

# 思路
1. notin子查询，筛选没下单的visit数据；
2. 左连，筛选左表-右表结果集；

# solution

## not in
```sql

select customer_id, count(visit_id) as count_no_trans
from Visits
where visit_id not in (
    select distinct visit_id
    from Transactions
)
group by customer_id
;

select customer_id, count(visit_id) as count_no_trans
from Visits
where visit_id not in (
    select visit_id
    from Transactions
    group by visit_id
)
group by customer_id
;
```

## left join
```sql
select customer_id, count(visit.visit_id) as count_no_trans
from Visits visit
         left join Transactions transaction
on (visit.visit_id = transaction.visit_id)
where transaction.amount is null
group by visit.customer_id
;
```