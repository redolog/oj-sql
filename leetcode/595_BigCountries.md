# 题目

[595. 大的国家](https://leetcode.cn/problems/big-countries/)

# 思路
1. 两个条件直接or；
2. 两个条件分别select，结果集去重union合并；

# solution

## or
```sql
select name,population,area from World
where area >= 3000000 or population >= 25000000;
```
## union
union会将多个结果集去重、合并。unionall则不会去重。
```sql
select name,population,area from World
where area >= 3000000
union
select name,population,area from World
where population >= 25000000;
```