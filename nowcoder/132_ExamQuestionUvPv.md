# 题目

[SQL132 每个题目和每份试卷被作答的人数和次数](https://www.nowcoder.com/practice/203d0aed8928429a8978185d9a03babc?tpId=240&tqId=2183297&ru=/exam/oj&qru=/ta/sql-advanced/question-ranking&sourceUrl=%2Fexam%2Foj%3Fpage%3D1%26tab%3DSQL%25E7%25AF%2587%26topicId%3D240)

# 思路
1. 分别查对应表，列对齐，union all
2. 统一排序，使用`LEFT (str, len)`提取各自id首值；


# solution

## 子查询分别排序 union
```sql
select * from (
  select
     exam_id as tid,
     count(distinct uid) as uv,
     count(id) as pv
  from exam_record
  group by exam_id
  order by uv desc,pv desc
) t1

union all

select * from (
  select
     question_id as tid,
     count(distinct uid) as uv,
     count(id) as pv
  from practice_record
  group by question_id
  order by uv desc,pv desc
) t2
;
```

## 统一排序，使用`LEFT (str, len)`提取各自id首值；
```sql
select 
  exam_id as tid,
  count(distinct uid) as uv,
  count(id) as pv
from exam_record
group by exam_id
union all
select 
  question_id as tid,
  count(distinct uid) as uv,
  count(id) as pv
from practice_record
group by question_id
-- 统一排序，left tid第一个数，区分两个表的数据
order by left(tid,1) desc,uv desc,pv desc
```
