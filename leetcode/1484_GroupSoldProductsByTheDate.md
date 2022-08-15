# 题目

[1484. Group Sold Products By The Date](https://leetcode.cn/problems/group-sold-products-by-the-date/)

# 思路
1. 以 sell_date groupby分组；
2. count去重计数；
3. group_concat 拼接单字段多值；

# solution

## groupby count distinct groupconcat
```sql
select
    sell_date,
    count(distinct product) as num_sold,
    GROUP_CONCAT(DISTINCT product ORDER BY product ASC  SEPARATOR',') as products
from Activities
group by sell_date;
```