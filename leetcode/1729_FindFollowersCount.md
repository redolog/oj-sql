# 题目

[1729. Find Followers Count](https://leetcode.cn/problems/find-followers-count/)

# 思路
1. group by 
2. count

# solution

## group by count 
```sql
select user_id, count(follower_id) as followers_count
from Followers
group by user_id
order by user_id
;
```