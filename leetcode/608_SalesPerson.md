# 题目

[607. 销售员](https://leetcode.cn/problems/sales-person/)

# 思路
1. 先查出red名公司对应订单，排除这些订单对应销售人员即可。

# solution

## subquery notin
```sql
select name
from SalesPerson
where sales_id not in (
    select distinct sales_id
    from Orders
    where com_id in (
        select com_id
        from Company
        where name = 'RED'
    )
);
```

