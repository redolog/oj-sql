# 题目

[1965. Employees With Missing Information](https://leetcode.cn/problems/employees-with-missing-information/)

# 思路
1. employee-salary union salary-employee 每个表中对方没有的数据合并
2. unionall两个表所有empId，count只有一个的就是所求

# solution

## union
```sql
select employee_id from (
    select e.employee_id
    from Employees e
    left join Salaries s
    on (s.employee_id = e.employee_id)
    where s.salary is null
    union
    select s.employee_id
    from Employees e
    right join Salaries s
    on (s.employee_id = e.employee_id)
    where e.name is null
) t_tmp
order by employee_id asc
;
```

## union all
```sql
select employee_id from (
    select employee_id from Employees
    # unionall 不去重，合并所有结果集，因此两个结果集count=1的，就是符合题干的数据
    union all
    select employee_id from Salaries
) t_tmp
group by employee_id
having count(employee_id)=1
order by employee_id asc
;
```