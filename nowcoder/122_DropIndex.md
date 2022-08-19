# 题目

[SQL122 删除索引](https://www.nowcoder.com/practice/4963f6d63dde48d787aaa2b43460fb4b?tpId=240&tqId=2223573&ru=/exam/oj&qru=/ta/sql-advanced/question-ranking&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D240)

# 思路
1. drop index;
2. 也可以使用alter语句修改表结构；

# solution

## drop index
```sql
drop index uniq_idx_exam_id on examination_info;
drop index full_idx_tag on examination_info;

alter table examination_info drop index uniq_idx_exam_id;
alter table examination_info drop index full_idx_tag;
```