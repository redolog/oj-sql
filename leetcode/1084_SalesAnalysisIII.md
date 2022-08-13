# 题目

[1084. 销售分析III](https://leetcode.cn/problems/sales-analysis-iii/)

# 思路
1. 先根据productId分组，分组内使用聚合函数筛选；

# solution

## group by max min
```sql
select product.product_id,product.product_name
from Sales sales
left join Product product
on (product.product_id = sales.product_id)
group by sales.product_id
having max(sales.sale_date)<='2019-03-31' and min(sales.sale_date)>='2019-01-01'
;
```