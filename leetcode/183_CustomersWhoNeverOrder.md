# 题目

[183. 从不订购的客户](https://leetcode.cn/problems/customers-who-never-order/)

# 考察点
1. 左连

# solution

## 左连
左连接保证左表结果一定查出，关联右表数据null时，对应右列null
```sql
select c.name as `Customers`
from Customers c
left join Orders o
on (c.id=o.customerId)
where o.id is null;
```

## 子查询id not in
join查出的是有下单的顾客数据，not in进行反选

```sql
select name as `Customers`
from Customers
where id not in (
    select c.id
    from Customers c
    join Orders o
    on (c.id=o.customerId)
);
```

内部子查询可简化为单表查：
```sql
select name as `Customers`
from Customers
where id not in (
    select customerId
    from Orders
);
```