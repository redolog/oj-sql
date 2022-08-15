# 题目

[1795. Rearrange Products Table](https://leetcode.cn/problems/rearrange-products-table/)

# 列转行思路
1. union
2. 每个select语句内只查一个列

# solution

## union
```sql
select
    product_id,
    'store1' as store,
    store1 as price
from Products
where store1 is not null

union

select
    product_id,
    'store2' as store,
    store2 as price
from Products
where store2 is not null

union

select
    product_id,
    'store3' as store,
    store3 as price
from Products
where store3 is not null
;
```