# 题目

[178. 分数排名](https://leetcode.cn/problems/rank-scores/)

# 考察点

1. 窗口函数
2. count计数+多表用作排名

# solution

## 使用dense_rank排名
[窗口函数介绍参见这里](../wiki/WindowFunction.md)

可用于排序、排名的窗口函数有：
- RANK
- DENSE_RANK
- PERCENT_RANK

本题应该用`DENSE_RANK`获取无缺口排名。

```sql
SELECT score,dense_rank() OVER(ORDER BY score DESC) as `rank`
FROM  Scores
```
学习了窗口函数后，排名问题直接用函数解决是最直观的。

## 使用多表count计数
在MySQL老版本还不支持窗口函数的背景下，我们也可以考虑用多个表，第二张表用于count计数。

```sql
SELECT 
       a.score ,
       (SELECT COUNT(DISTINCT b.score) FROM Scores b WHERE b.score>=a.score) as `rank`
FROM Scores a
ORDER BY a.score DESC;
```