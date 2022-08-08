# 题目

[196. 删除重复的电子邮箱](https://leetcode.cn/problems/delete-duplicate-emails/)

# 思路
这道题本质上是：查出重复的邮箱。同时，保留最小id的一条。

基于 [182_DuplicateEmails](182_DuplicateEmails.md) 我们查重复的sql有了，保留最小id，我们可以使用min函数。

同时，以上过程，可以用窗口函数来搞定：同一个邮箱分区，分区内有排行信息。

# solution

## count having min
使用CTE暂存最小id、重复邮箱。
```sql
with duplicate as (
    select min(id) as id,email
    from Person
    group by email
    having count(email)>1
)

delete from Person
where email in (
    select email from duplicate
) and id not in (
    select id from duplicate
);
```

## 使用 rank函数
```sql
delete from person
where id in
      (
          select 
                 id 
          from
            (select id, dense_rank() over(partition by email order by id) rnk 
          from person) t 
            where rnk > 1
      )
```