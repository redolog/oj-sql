# 题目

[596. 超过5名学生的课](https://leetcode.cn/problems/classes-more-than-5-students/)

# 思路
1. 先groupby，再直接having；
2. groupby之后求count，子查询筛选cnt；

# solution

## groupby & having
```sql
select class from Courses
group by class
having count(distinct student)>=5;
```
## groupby & subquery
```sql
select class
from (
         select class,count(distinct student) cnt
         from Courses
         group by class
     ) t
where cnt>=5;
```