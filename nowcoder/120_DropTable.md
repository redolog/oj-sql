# 题目

[SQL120 删除表](https://www.nowcoder.com/practice/df2f634a53324bbd9369fe6723fedc49?tpId=240&tqId=2223568&ru=/exam/oj&qru=/ta/sql-advanced/question-ranking&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D240)

# 思路
1. drop table删除表；

# solution

## drop table
```sql
drop table if exists exam_record_2011,exam_record_2012,exam_record_2013,exam_record_2014;
```

## 也可以写成脚本
```sql
SELECT concat('drop table if exists ',GROUP_CONCAT('',' ',TABLE_NAME),';') AS sqltext into @sqltext 
FROM information_schema.TABLES 
WHERE TABLE_NAME LIKE 'exam_record_201_' and substr(TABLE_NAME,13,4) between 2011 and 2014;

PREPARE stmt FROM @sqltext;
EXECUTE stmt ;
DEALLOCATE PREPARE stmt;
```