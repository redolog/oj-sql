# 题目

[SQL128 未完成试卷数大于1的有效用户](https://www.nowcoder.com/practice/46cb7a33f7204f3ba7f6536d2fc04286?tpId=240&tqId=2183007&ru=/exam/oj&qru=/ta/sql-advanced/question-ranking&sourceUrl=%2Fexam%2Foj%3Fpage%3D1%26tab%3DSQL%25E7%25AF%2587%26topicId%3D240)

# 思路
1. having筛选分组条件；
2. sum if筛选不同条件下的计数；
3. groupconcat拼接多个值到一个字段上；


# solution

## sum if groupconcat concat dateformat having
```sql
select
   uid,
   sum(if(submit_time is null,1,null)) incomplete_cnt,
   sum(if(submit_time is null,null,1)) complete_cnt,
   group_concat(distinct concat(date_format(start_time, '%Y-%m-%d'),':',tag) separator ';') detail
from exam_record re
left join examination_info info
on (re.exam_id=info.exam_id)
where year(re.start_time)=2021
group by uid
having incomplete_cnt between 2 and 4 and complete_cnt>=1
order by incomplete_cnt desc
;

```