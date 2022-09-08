# 题目

[SQL134 满足条件的用户的试卷完成数和题目练习数](https://www.nowcoder.com/practice/5c03f761b36046649ee71f05e1ceecbf?tpId=240&tqId=2183299&ru=/exam/oj&qru=/ta/sql-advanced/question-ranking&sourceUrl=%2Fexam%2Foj%3Fpage%3D1%26tab%3DSQL%25E7%25AF%2587%26topicId%3D240)

# 思路
1. 根据条件先筛出符合条件的uid；
2. 两个表分别groupby统计，leftjoin连起来，合成最后的结果集；


# solution

## leftjoin if is null groupby orderby
```sql
with valid_ids as (
    select user.uid uid
    from exam_record record
    join user_info user
    on (record.uid = user.uid)
    where record.exam_id=9001 and user.level=7
    group by uid
    having avg(score)>=80
)

select
    uid,
    exam_cnt,
    if(question_cnt is null ,0 ,question_cnt)
from (
      (select
           uid,
           count(id) exam_cnt
       from exam_record
       where year(submit_time)=2021
       group by uid ) t_exam
      left join
     (select
          uid,
          count(id) question_cnt
      from practice_record
      where year(submit_time)=2021
      group by uid ) t_practice
     using (uid)
         )
where uid in (
    select uid from valid_ids
)
order by exam_cnt asc, question_cnt desc;
```
