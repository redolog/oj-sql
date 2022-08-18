# 题目

[SQL110 插入记录（一）](https://www.nowcoder.com/practice/5d2a42bfaa134479afb9fffd9eee970c?tpId=240&tqId=2221797&ru=/exam/oj&qru=/ta/sql-advanced/question-ranking&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D240)

# 思路
1. 简单插入语句；

# solution

## insert into
```sql
insert into exam_record (uid, exam_id, start_time, submit_time, score)
values
    (1001, 9001, '2021-09-01 22:11:12', '2021-09-01 23:01:12', 90),
    (1002, 9002, '2021-09-04 07:01:02', null, null);
```