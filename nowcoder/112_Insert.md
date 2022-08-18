# 题目

[SQL111 插入记录（三）](https://www.nowcoder.com/practice/978bcee6530a430fb0be716423d84082?tpId=240&tqId=2223556&ru=/exam/oj&qru=/ta/sql-advanced/question-ranking&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D240)

# 思路
1. 替换插入语句；

# solution

## replace into
```sql
replace into examination_info (exam_id,tag,difficulty,duration,release_time)
values (9003,'SQL','hard',90,'2021-01-01 00:00:00');
```

## 先delete再insert
```sql
delete from examination_info where exam_id = 9003;
insert into examination_info (exam_id,tag,difficulty,duration,release_time)
values (9003,'SQL','hard',90,'2021-01-01 00:00:00');
```