# 题目

[176. 第二高的薪水](https://leetcode.cn/problems/second-highest-salary/)

# 考察点

1. 排序
2. 去重
3. 空处理

# 使用desc倒序
limit限制条数，offset指定偏移量。

```sql
SELECT ifnull((
    SELECT DISTINCT salary
    FROM Employee
    ORDER BY salary DESC
    LIMIT 1 OFFSET 1 ),null) AS SecondHighestSalary;
```
