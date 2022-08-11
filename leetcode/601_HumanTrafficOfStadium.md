# 题目

[601. 体育馆的人流量](https://leetcode.cn/problems/human-traffic-of-stadium/)

# 思路
1. 使用`id-row_number`可以判断是否为连续序列；
2. 基于上述sn值，分组，并且having判断count，即可判断连续了多少条；

# solution

## col-row_number & groupby having
```sql
# 统计序列值，id-rowNumber 相等，说明是连续序列
with t_sn as (
    select *, id-row_number() over(order by id) as sn
    from stadium
    where people >=100
)
select id,visit_date,people
from t_sn
where sn in (
    select sn
    from t_sn
    group by sn
    having count(sn)>=3
);
```