# 题目

[182. 查找重复的电子邮箱](https://leetcode.cn/problems/duplicate-emails/)

# 考察点
1. groupby，having条件
2. 子查询count

# solution

## 使用group by having

```sql
select email as `Email`
from Person
group by email
having count(email)>1;
```

## 使用子查询count

```sql
select t.email as `Email`
from (
    select email,count( email) as cnt
    from Person
    group by email
) t
where t.cnt>1;
```