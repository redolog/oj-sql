# 题目

[197. 上升的温度](https://leetcode.cn/problems/rising-temperature/)

# 思路
需要借助日期函数：`datediff`，可进行date类型间的减法。

# solution

## datediff join
自连，然后一个表示前一天，一个代表后一天。

前后一天使用`datediff`==1或者==-1判断。
```sql
select `after`.id
from Weather `before`
join Weather `after`
on (datediff(`before`.recordDate,`after`.recordDate)=-1)
where `before`.temperature<`after`.temperature;
```