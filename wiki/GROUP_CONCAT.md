# GROUP_CONCAT 函数
> The GROUP_CONCAT() function in MySQL is used to concatenate data from multiple rows into one field. This is an aggregate (GROUP BY) function which returns a String value, if the group contains at least one non-NULL value. Otherwise, it returns NULL.
> 
聚合函数，将多行同列值合并为一个字段。

## 语法
```sql
SELECT col1, col2, ..., colN
    GROUP_CONCAT ( [DISTINCT] col_name1
    [ORDER BY clause]  [SEPARATOR str_val] )
FROM table_name GROUP BY col_name2; 
```

## 例子
[1484_GroupSoldProductsByTheDate](/leetcode/1484_GroupSoldProductsByTheDate.md)
