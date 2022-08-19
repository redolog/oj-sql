# 题目

[SQL124 统计作答次数](https://www.nowcoder.com/practice/45a87639110841b6950ef6a12d20175f?tpId=240&tqId=2180960&ru=/exam/oj&qru=/ta/sql-advanced/question-ranking&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D240)

# 思路
1. count sum if；

# solution

## count sum if
```sql
select
    count(exam_id) total_pv,
    sum(if(submit_time is null or score is null,0,1)) complete_pv,
    count(distinct if(submit_time is not null, exam_id,null)) complete_exam_cnt
from exam_record;
```