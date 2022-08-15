# 题目

[1693. Daily Leads and Partners](https://leetcode.cn/problems/daily-leads-and-partners/)

# 思路
1. group by 多个key
2. 再根据计数字段进行去重count

# solution

## group by count distinct
```sql
select
   date_id,
   make_name,
   count(distinct lead_id) as unique_leads,
   count(distinct partner_id) as unique_partners
from DailySales
group by date_id, make_name
```