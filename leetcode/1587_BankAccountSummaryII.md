# 题目

[1587. Bank Account Summary II](https://leetcode.cn/problems/bank-account-summary-ii/)

# 思路
1. groupby 然后having通过sum筛选，account转name可以用子查询；
2. 连表也可以；

# solution

## not in
```sql
select
        (select name from Users u where u.account=t.account) as name,
        sum(t.amount) as balance
from Transactions t
group by t.account
having sum(t.amount)>10000;
```