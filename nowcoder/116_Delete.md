# 题目

[SQL116 删除记录（二）](https://www.nowcoder.com/practice/964c9f7fffbb4ab18b507cfed4111b4a?tpId=240&tqId=2223562&ru=/exam/oj&qru=/ta/sql-advanced/question-ranking&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D240)

# 思路
1. 简单删除语句；

# solution

## delete where limit
```sql
delete from exam_record
where submit_time is null or timestampdiff(minute,start_time,submit_time)<5
order by start_time
limit 3;
```
