# 题目

[1148. 文章浏览 I](https://leetcode.cn/problems/article-views-i/)

# 思路
1. 先筛选，再去重；

# solution

## where distinct
```sql
select distinct author_id as id
from Views
where author_id=viewer_id
order by id asc
;
```