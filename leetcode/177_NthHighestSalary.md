# 题目

[177. 第N高的薪水](https://leetcode.cn/problems/nth-highest-salary/)

# 考察点

1. 函数定义
2. 变量定义
3. 基于`group by`的排序，解决同名同级问题
4. 窗口函数

# solution
## 使用desc倒序
- limit限制条数，offset指定偏移量。
- offset需在函数内通过变量的方式进行一次定义。
- 通过offset偏移的方式进行排序，同时使用`group by`来进行去重，保证`byKey`是排序的键。

```sql
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
    # 设置偏移量，下方sql中无法直接 N-1
    SET N := N-1;
RETURN (
      SELECT 
            salary
      FROM 
            employee
      GROUP BY 
            salary
      ORDER BY 
            salary DESC
      LIMIT N, 1
    );
END
```

## 使用dense_rank排名
[窗口函数介绍参见这里](../wiki/WindowFunction.md)

可用于排序、排名的窗口函数有：
- RANK
- DENSE_RANK
- PERCENT_RANK

本题应该用`DENSE_RANK`获取无缺口排名。

```sql
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
  RETURN (
        SELECT 
            DISTINCT salary
        FROM 
            (SELECT 
                salary, DENSE_RANK() over(ORDER BY salary DESC) AS rnk
             FROM 
                employee) t_tnk
        WHERE rnk = N
  );
END
```
