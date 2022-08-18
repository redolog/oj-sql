# 题目

[SQL115 删除记录（一）](https://www.nowcoder.com/practice/d331359c5ca04a3b87f06b97da42159c?tpId=240&tqId=2223561&ru=/exam/oj&qru=/ta/sql-advanced/question-ranking&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D240)

# 思路
1. 简单删除语句；
2. timestampdiff 可取日期差值分钟数；

# solution

## delete where timestampdiff
```sql
delete from exam_record
where timestampdiff(MINUTE,start_time,submit_time)<5 and score<60;
```
