# 题目

[SQL119 修改表](https://www.nowcoder.com/practice/d08209df6f464cebafda5dfd5de03fce?tpId=240&tqId=2223567&ru=/exam/oj&qru=/ta/sql-advanced/question-ranking&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D240)

# 思路
1. alter table修改字段schema；

# solution

## alter table
```sql
ALTER TABLE user_info ADD school varchar(15) AFTER `level`;
ALTER TABLE user_info CHANGE job profession varchar(10);
ALTER TABLE user_info CHANGE COLUMN achievement achievement int DEFAULT 0;
```
