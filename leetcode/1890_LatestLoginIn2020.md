# 题目

[1890. The Latest Login in 2020](https://leetcode.cn/problems/the-latest-login-in-2020/)

# 列转行思路
1. groupby 之后取max

# solution

## groupby max
```sql
select user_id, max(time_stamp) as last_stamp
from Logins
where time_stamp between '2020-01-01' and '2021-01-01'
group by user_id
;
```