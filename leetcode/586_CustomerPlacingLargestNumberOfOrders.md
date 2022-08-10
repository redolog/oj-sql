# 题目

[586. 订单最多的客户](https://leetcode.cn/problems/customer-placing-the-largest-number-of-orders/)

# 思路
1. 先groupby，再count，排序，取头一条；
2. 进阶问题，可利用groupby之后的having条件语句，利用count等值或者all语句取多条排名一致的数据；

# solution

## 先groupby再order，最后limit
```sql
select customer_number
from (
         select customer_number,count(customer_number) cnt
         from Orders
         group by customer_number
     ) t
order by cnt desc
limit 1;
```
实际上这里可以不用子查询，直接在一层语句上排序。

```sql
select customer_number
from Orders
group by customer_number
order by count(customer_number) desc
limit 1;
```

## having条件语句
子查询中根据分组排序结果，拿到最多销量的值，外部having匹配销量。
```sql
select customer_number
from Orders
group by customer_number
having count(*)=(
    select count(*)
    from Orders
    group by customer_number
    order by count(*) desc
    limit 1
    );
```

这里也可以借助all子查询语句：
这里表示count需要大于等于子查询中每一条count才行。
```sql
select customer_number
from Orders
group by customer_number
having count(*)>=all(
    select count(*)
    from Orders
    group by customer_number
);
```