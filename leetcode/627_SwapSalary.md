# 题目

[627. 变更性别](https://leetcode.cn/problems/swap-salary/)

# 思路
1. update条件，用if分支；
2. 也可以用switchcase分支；

# solution

## if
```sql
update Salary
set sex=if(sex='m','f','m')
;
```

## case when
```sql
update Salary
set sex =
        (
            case sex
                when 'm' then 'f'
                else 'm'
            end
        )
;
```