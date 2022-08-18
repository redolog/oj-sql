# 题目

[SQL114 更新记录（二）](https://www.nowcoder.com/practice/0c2e81c6b62e4a0f848fa7693291defc?tpId=240&tqId=2223560&ru=/exam/oj&qru=/ta/sql-advanced/question-ranking&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D240)

# 思路
1. 简单更新语句；

# solution

## update where
```sql
update exam_record
set
    submit_time='2099-01-01 00:00:00',
    score=0
where start_time<'2021-09-01 00:00:00' and score is null;
```
