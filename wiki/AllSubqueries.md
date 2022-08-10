# all 子查询语句

[MySQL官方文档：13.2.11.4 Subqueries with ALL
](https://dev.mysql.com/doc/refman/8.0/en/all-subqueries.html)

# 语法
```sql
operand comparison_operator ALL (subquery)
```

示例：
```sql
SELECT s1 FROM t1 WHERE s1 > ALL (SELECT s1 FROM t2);
```

用法：
all关键字前为比较符，之后为参与比较的子查询结果。

与普通子查询的区别：
```sql
SELECT * FROM t1 WHERE 1 > (SELECT s1 FROM t2);
```
当t2空时，普通子查询返回null，因为判定比较结果为false。

但是all语句，t2空时判定比较结果为true，查询出t1所有数据。