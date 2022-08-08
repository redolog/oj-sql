# with 语句
# CTE CommonTableExpression

[MySQL官方cte文档：13.2.15 WITH (Common Table Expressions)](https://dev.mysql.com/doc/refman/8.0/en/with.html)

# 基础理解
with语句是cte的语法关键字，通过cte，我们可以暂存一段statement的resultset，就像定义了一个临时表（变量），后续sql可像操作表一样操作这个临时表。

## 举例
```sql
WITH
  cte1 AS (SELECT a, b FROM table1),
  cte2 AS (SELECT c, d FROM table2)
SELECT b, d FROM cte1 JOIN cte2
WHERE cte1.a = cte2.c;
```
如上sql定义了两个cte，在下方的select中，可以当做两个表来操作。

实例如 [184. 部门工资最高的员工](../leetcode/184_DepartmentHighestSalary.md) ，使用with的解法，我们先暂存了最高薪水与对应部门id，后续可直接连表、条件查询。

## with语法
1. SELECT, UPDATE, DELETE 语句之前
```sql
WITH ... SELECT ...
WITH ... UPDATE ...
WITH ... DELETE ...
```
2. 子查询之前
```sql
SELECT ... WHERE id IN (WITH ... SELECT ...) ...
SELECT * FROM (WITH ... SELECT ...) AS dt ...
```
3. 包含select语句，select关键字之前
```sql
INSERT ... WITH ... SELECT ...
REPLACE ... WITH ... SELECT ...
CREATE TABLE ... WITH ... SELECT ...
CREATE VIEW ... WITH ... SELECT ...
DECLARE CURSOR ... WITH ... SELECT ...
EXPLAIN ... WITH ... SELECT ...
```
4. 同级只允许一个with，如下为**非法示例**：
```sql
WITH cte1 AS (...) WITH cte2 AS (...) SELECT ...
```
5. 不同级可存在不同的with
```sql
WITH cte1 AS (SELECT 1)
SELECT * FROM (WITH cte2 AS (SELECT 2) SELECT * FROM cte2 JOIN cte1) AS dt;
```
6. 同一个上下文下，cte命名是唯一的

# 高级用法
## 可嵌套
多个cte之间可直接引用。甚至某个cte可直接递归调用自身。

## 递归cte
嵌套递归cte：定义了一个cte，在其子查询中可直接引用该cte。

递归语句必须以`WITH RECURSIVE`开头。

### 举例：
```sql
WITH RECURSIVE cte (n) AS
(
  SELECT 1
  UNION ALL
  SELECT n + 1
  FROM cte 
  # 递归一定要有边界条件！！
  WHERE n < 5
)
SELECT * FROM cte;
```

结果：
```csv
+------+
| n    |
+------+
|    1 |
|    2 |
|    3 |
|    4 |
|    5 |
+------+
```

### 结构
```sql
SELECT ...      -- return initial row set
UNION ALL
SELECT ...      -- return additional row sets
```
如上，第一个`select`定义初始状态，通过`union/union all`连接初始、递推状态，第二个`select`则表示递推状态。

如果使用`UNION DISTINCT`连接状态，重复数据会被消除。

### 字段类型、长度
看一个例子：
```sql
WITH RECURSIVE cte AS
(
  SELECT 1 AS n, 'abc' AS str
  UNION ALL
  SELECT n + 1, CONCAT(str, str) FROM cte WHERE n < 3
)
SELECT * FROM cte;
```
非严格模式下输出：
```csv
+------+------+
| n    | str  |
+------+------+
|    1 | abc  |
|    2 | abc  |
|    3 | abc  |
+------+------+
```
严格模式下报错：
```log
ERROR 1406 (22001): Data too long for column 'str' at row 1
```

以上两种输出的原因是，定义cte时，str变量默认为`CHAR(3)`，长度已被固定，因此非严格模式下输出都是`abc`，因为后续拼接的字符全被截断了，而严格模式下检测到超长就报错。

一种解决办法是，定义cte时，我们指定一个更长的类型：
```sql
WITH RECURSIVE cte AS
(
  SELECT 1 AS n, CAST('abc' AS CHAR(20)) AS str
  UNION ALL
  SELECT n + 1, CONCAT(str, str) FROM cte WHERE n < 3
)
SELECT * FROM cte;
```
输出如下：
```csv
+------+--------------+
| n    | str          |
+------+--------------+
|    1 | abc          |
|    2 | abcabc       |
|    3 | abcabcabcabc |
+------+--------------+
```

### 递归cte禁止的操作
递归的`select`中禁止有如下操作：
```sql
聚合函数，如 SUM()

窗口函数，如 rank()

GROUP BY

ORDER BY

DISTINCT
```

`LIMIT`关键字在 MySQL 8.0.19 版本中才允许在cte中使用。

### 退出条件
递归必须要有边界退出条件。

同时，系统也提供了几种兜底的参数，防止递归调用无限执行。

- `cte_max_recursion_depth` 可指定最大递归深度。
- `max_execution_time` 可指定单次执行时长，默认为1000ms。
- MySQL 8.0.19开始，可以在递推`select`中使用`LIMIT`限制条数。

可针对单次`session`指定参数：
```sql
SET SESSION cte_max_recursion_depth = 10;      -- permit only shallow recursion
SET SESSION cte_max_recursion_depth = 1000000; -- permit deeper recursion
```
也可以在对应cte语句中指定限制参数：
```sql
WITH RECURSIVE cte (n) AS
(
  SELECT 1
  UNION ALL
  SELECT n + 1 FROM cte
)
SELECT /*+ SET_VAR(cte_max_recursion_depth = 1M) */ * FROM cte;

WITH RECURSIVE cte (n) AS
(
  SELECT 1
  UNION ALL
  SELECT n + 1 FROM cte
)
SELECT /*+ MAX_EXECUTION_TIME(1000) */ * FROM cte;
```

# 实例
官方文档提供了几个实例：[生成Fibonacci序列](https://dev.mysql.com/doc/refman/8.0/en/with.html#common-table-expressions-recursive-fibonacci-series) 。