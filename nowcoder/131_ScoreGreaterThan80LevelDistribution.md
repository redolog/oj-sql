# 题目

[SQL131 作答试卷得分大于过80的人的用户等级分布](https://www.nowcoder.com/practice/5bc77e3a3c374ad6a92798f0ead4c744?tpId=240&tqId=2183024&ru=/exam/oj&qru=/ta/sql-advanced/question-ranking&sourceUrl=%2Fexam%2Foj%3Fpage%3D1%26tab%3DSQL%25E7%25AF%2587%26topicId%3D240)

# 思路
1. 连表
   1. 对每个表条件筛选
   2. 聚合、排序


# solution

## join table
```sql
select
   user.level,
   count(record.id) as level_cnt
from exam_record record
join examination_info info
on (record.exam_id=info.exam_id)
join user_info user
on (record.uid=user.uid)
where info.tag='SQL'
and record.score >80
group by user.level
order by level_cnt desc
;
```
