# 题目

[620. 有趣的电影](https://leetcode.cn/problems/not-boring-movies/)

# 思路
1. 简单查询，筛选条件即可，其中判断奇偶数可以使用mod函数；

# solution

## simple query
```sql
select id,movie,description,rating
from cinema
where id%2=1 and description!='boring'
order by rating desc;

select id,movie,description,rating
from cinema
where mod(id,2)=1 and description!='boring'
order by rating desc;
```