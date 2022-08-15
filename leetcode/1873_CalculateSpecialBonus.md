# 题目

[1873. Calculate Special Bonus](https://leetcode.cn/problems/calculate-special-bonus/)

# 列转行思路
1. 分支判断，用if casewhen均可
2. 判断奇偶数使用 %2=1 or mod(col,2)=1 均可

# solution

## if
```sql
select
    employee_id,
    if( employee_id%2=1 and left(name,1)!='M',salary, 0) as bonus
from Employees
order by employee_id asc;

select
    employee_id,
    if( mod(employee_id,2)=1 and left(name,1)!='M',salary, 0) as bonus
from Employees
order by employee_id asc;

SELECT
    employee_id,
    CASE WHEN
     MOD(employee_id, 2) = 1 AND name not rlike '^M' 
    THEN salary 
    ELSE 0 
    END AS bonus
FROM Employees
ORDER BY employee_id;
```