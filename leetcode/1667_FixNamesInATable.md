# 题目

[1667. Fix Names in a Table](https://leetcode.cn/problems/fix-names-in-a-table/)

# 思路
1. 主要考察sql字符串处理函数
   1. concat 拼接多个串
   2. substring 截取子串
   3. left 从左截取子串
   4. right 从右截取子串
   5. 注意sql下标从1开始
   6. upper 转大写
   7. lower 转小写

# solution

## concat substring upper lower
```sql
select
    user_id,
    concat(upper(substring(name,1,1)), lower(substring(name,2))) as name
from Users
order by user_id asc;

select
    user_id,
    concat(upper(left(name,1)), lower(substring(name,2))) as name
from Users
order by user_id asc;
```