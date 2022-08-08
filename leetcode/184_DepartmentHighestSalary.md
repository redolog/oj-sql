# 题目

[184. 部门工资最高的员工](https://leetcode.cn/problems/department-highest-salary/)

# 思路
1. 先查出各部门最高薪水
2. 找到对应各部门最高薪水的人

# solution

## with CTE
使用CTE，我们可以暂存第一步的信息，第二步连表、条件找对应人即可。
```sql
with report as (
    select e.departmentId,max(e.salary) as maxSalary
    from Employee e
    group by e.departmentId
)

select d.name as `Department`,e.name as `Employee`,e.salary as `Salary`
from Employee e
join Department d
  on (e.departmentId=d.id)
join report
  on (report.maxSalary=e.salary and report.departmentId = e.departmentId)
```

## 子查询
上述解法中的with部分，也可以使用子查询代替，sql看起来会结构嵌套多一些。

同时这里的in还用到了多个参数一起in，属实不常见。

```sql
SELECT
    Department.name AS 'Department',
    Employee.name AS 'Employee',
    Salary
FROM
    Employee
JOIN
    Department 
ON Employee.DepartmentId = Department.Id
WHERE
        (Employee.DepartmentId , Salary) IN
        (   SELECT
                DepartmentId, MAX(Salary)
            FROM
                Employee
            GROUP BY DepartmentId
        )
;
```