# 题目

[SQL133 分别满足两个活动的人](https://www.nowcoder.com/practice/a126cea91d7045e399b8ecdcadfb326f?tpId=240&tqId=2183298&ru=/exam/oj&qru=/ta/sql-advanced/question-ranking&sourceUrl=%2Fexam%2Foj%3Fpage%3D1%26tab%3DSQL%25E7%25AF%2587%26topicId%3D240)

# 思路
1. 活动1，groupby uid之后，having min最小分数；
2. 活动2，连表后，timestampdiff 筛选分数时间差；


# solution

## groupby min join timestampdiff
```sql
select
    uid,
    'activity1' as activity
from exam_record
group by uid
having min(score)>=85

union all

select
    distinct uid,
    'activity2' as activity
from exam_record record
join examination_info info
on (record.exam_id = info.exam_id)
where info.difficulty='hard'
  and record.score>80
  and timestampdiff(MINUTE,record.start_time,record.submit_time)*2<info.duration
order by uid
```
