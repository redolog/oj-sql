# 题目

[SQL130 试卷发布当天作答人数和平均分](https://www.nowcoder.com/practice/5b58e89556dc4153a79d8cf8c08ba499?tpId=240&tqId=2183023&ru=/exam/oj&qru=/ta/sql-advanced/question-ranking&sourceUrl=%2Fexam%2Foj%3Fpage%3D1%26tab%3DSQL%25E7%25AF%2587%26topicId%3D240)

# 思路
1. 连表
   1. sum 求和
   2. avg 求均值
   3. round 小数保留n位
2. 不连表


# solution

## join table
```sql
select
    record.exam_id,
    count(distinct record.uid) as uv,
    round(avg(record.score),1) as avg_score
from examination_info exam
join exam_record record
on (exam.exam_id=record.exam_id)
join user_info user
on (record.uid=user.uid)
where exam.tag='SQL'
  and user.level>5
group by record.exam_id
order by uv desc, avg_score asc
```

## subquery
```sql
select
    exam_id,
    count(distinct uid) as uv,
    round(avg(score),1) as avg_score
from exam_record
where uid in (
    select uid from user_info where level>5
) 
and exam_id in (
    select exam_id from examination_info where tag='SQL'
)
group by exam_id
order by uv desc, avg_score asc;
```