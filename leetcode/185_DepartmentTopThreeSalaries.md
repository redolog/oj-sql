# 题目

[185. 部门工资前三高的所有员工](https://leetcode.cn/problems/department-top-three-salaries/)

# 思路
与 [178_RankScores](178_RankScores.md) 类似，我们先使用`dense_rank`查出对应排行。后面就是一个排行条件。

# solution

## dense_rank + cte
使用CTE暂存排行数据。
```sql
with t_rnk as (
    select id,name,salary,departmentId,DENSE_RANK() over(PARTITION BY departmentId ORDER BY salary DESC) AS rnk
    from Employee 
)

select d.name as `Department`,e.name as `Employee`,e.salary as `Salary`
from Employee e
join Department d
on (e.departmentId=d.id)
WHERE e.id in (select id from t_rnk where rnk<=3);
```

## 使用多表count计数
当然了，没有窗口函数前，我们也可以用多表计数来模拟排行。

```sql
with t_rnk as (
    SELECT
        a.id,
        (SELECT COUNT(DISTINCT b.salary) FROM Employee b WHERE b.departmentId=a.departmentId and b.salary>=a.salary) as rnk
    FROM Employee a
    ORDER BY a.salary DESC
)


select d.name as `Department`,e.name as `Employee`,e.salary as `Salary`
from Employee e
         join Department d
              on (e.departmentId=d.id)
WHERE e.id in (select id from t_rnk where rnk<=3);
```

## 多表count计数+子查询
官解的思路，使用a/b两个表，b表count进行计数计算排行（相当于每个a的数据都要进行一次比对操作）。

此方法效率较低，为`O(n^2)`。

有了排行后，我们将排行字句放入子查询，只要前三的数据：
```sql
SELECT
    d.Name AS 'Department', e1.Name AS 'Employee', e1.Salary
FROM
    Employee e1
        JOIN
    Department d ON e1.DepartmentId = d.Id
WHERE
    3 > (SELECT
            COUNT(DISTINCT e2.Salary)
        FROM
            Employee e2
        WHERE
            e2.Salary > e1.Salary
                AND e1.DepartmentId = e2.DepartmentId
        )
;
```