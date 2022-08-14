# 题目

[1179. Reformat Department Table](https://leetcode.cn/problems/reformat-department-table/)

# 思路
1. 先groupby，再增加12个虚拟列，使用if判断当前是否有值，针对某个月内的值，使用聚合函数sum汇总；

# solution

## groupby if sum
```sql
select
    id,
    sum(if(month='Jan',revenue,null)) as Jan_Revenue,
    sum(if(month='Feb',revenue,null)) as Feb_Revenue,
    sum(if(month='Mar',revenue,null)) as Mar_Revenue,
    sum(if(month='Apr',revenue,null)) as Apr_Revenue,
    sum(if(month='May',revenue,null)) as May_Revenue,
    sum(if(month='Jun',revenue,null)) as Jun_Revenue,
    sum(if(month='Jul',revenue,null)) as Jul_Revenue,
    sum(if(month='Aug',revenue,null)) as Aug_Revenue,
    sum(if(month='Sep',revenue,null)) as Sep_Revenue,
    sum(if(month='Oct',revenue,null)) as Oct_Revenue,
    sum(if(month='Nov',revenue,null)) as Nov_Revenue,
    sum(if(month='Dec',revenue,null)) as Dec_Revenue

from Department
group by id;
```