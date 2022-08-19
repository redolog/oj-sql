# 题目

[SQL125 得分不小于平均分的最低分](https://www.nowcoder.com/practice/3de23f1204694e74b7deef08922805b2?tpId=240&tqId=2180961&ru=/exam/oj&qru=/ta/sql-advanced/question-ranking&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D240)

# 思路
1. 先求平均数，再子查询条件筛选；

# solution

## min avg subquery
```sql
with t_avg_score as (
    select avg(score) avg_score
    from exam_record record
    join examination_info info
    using (exam_id)
    where info.tag='SQL'
)
select min(score) min_score_over_avg
from exam_record
join examination_info info
using (exam_id)
where info.tag='SQL' and score >= (select avg_score from t_avg_score)
;
```
也可以通过limit取结果集头一条：
```sql

with t_avg_score as (
    select
        avg(score) avg_score
    from exam_record record
    join examination_info info
    using (exam_id)
    where info.tag='SQL' 
)
select score min_score_over_avg
from exam_record 
join examination_info info
using (exam_id)
where info.tag='SQL' and score >= (select avg_score from t_avg_score)
order by score asc
limit 1
;
```