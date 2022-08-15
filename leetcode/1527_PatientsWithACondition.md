# 题目

[1527. Patients With a Condition](https://leetcode.cn/problems/patients-with-a-condition/)

# 思路
1. like模糊匹配；
2. 正则匹配；

# solution

## like
```sql
select *
from Patients
where conditions like '% DIAB1%' or conditions like 'DIAB1%' ;
```

## 正则
```sql
SELECT * FROM Patients
# \s 匹配空格，\\sDIAB1 匹配后面的 DIAB1
# ^DIAB1 匹配 DIAB1开头的
WHERE conditions REGEXP '^DIAB1|\\sDIAB1'
```
`rlike` 等价于 `REGEXP`。