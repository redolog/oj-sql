# 题目

[626. 换座位](https://leetcode.cn/problems/exchange-seats/)

# 思路
1. 使用窗口函数 lag、lead 查前序后序值；
2. 使用if isnull判空；
3. 窗口函数null时默认值；
---
1. 也可以考虑使用奇偶性判断，奇数id变为id+1，偶数id则变为id-1；
2. 针对最后一个奇数id，可进行特判；

# solution

## mod lead lag if isnull
```sql
# Write your MySQL query statement below

with report as (
    select 
        id,
        if(mod(id,2)=1,lead(student) over (order by id),lag(student) over (order by id)) student
    from Seat
)

select
    id,
    if(isnull(
               student
           ),(select student from Seat where id=report.id),student) as student
from report
order by id asc;
```

## lead lag with default arg
查询lead、lag文档可知：
- 第一个参数表示取哪个字段的值进行排列；
- 第二个参数表示分区、分组大小；
- 第三个参数表示null时所取默认值；

这里我们直接用lead设置最后一个奇数项的默认值即可，比使用if isnull判断简单很多。
```sql
select 
    id,
    if(mod(id,2)=1,lead(student,1,student) over (order by id),lag(student) over (order by id)) student
from Seat
```


## if判断奇偶数，交换id
```sql
with maxId as (
    select max(id) mid from Seat
)

select 
    if(
        mod(id,2)=1,
        if(id=maxId.mid,id,id+1),
        id-1) as id,
    student
from Seat,maxId
order by id asc;
```
上述写法等价于子查询写法：
```sql
select 
    if(
        mod(id,2)=1,
        if(id=(select max(id) from Seat),id,id+1),
        id-1) as id,
    student
from Seat
order by id asc;
```