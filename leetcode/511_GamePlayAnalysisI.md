# 题目

[511. 游戏玩法分析 I](https://leetcode.cn/problems/game-play-analysis-i/)

# 思路
1. 直接使用groupby分组，分组内使用min取最小date；
2. 也可以使用窗口函数partitionby分组，结果集存第一个date值，外部一个查询去重；

# solution

## groupby min
```sql
select
    player_id ,
    min(event_date) as 'first_login'
from Activity
group by player_id
```
## firstvalue partitionby distinct
```sql
with playerId2FirstDate as (
    select
        player_id ,
        FIRST_VALUE(event_date)  OVER (partition by player_id order by event_date asc) as 'first_login'
    from Activity
)
select distinct * from playerId2FirstDate;
```