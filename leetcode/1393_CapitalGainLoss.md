# 题目

[1393. Capital Gain/Loss](https://leetcode.cn/problems/capital-gainloss/)

# 思路
1. 先groupby，再sum汇总，其中的值正负使用if判断即可。

# solution

## groupby if sum
```sql
select
    stock_name ,
    sum(if(operation='Sell',price,-price)) as capital_gain_loss
from Stocks
group by stock_name;
```