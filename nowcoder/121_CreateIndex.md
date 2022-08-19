# 题目

[SQL121 创建索引](https://www.nowcoder.com/practice/f2ea9ccf33c740d58576608940981807?tpId=240&tqId=2223570&ru=/exam/oj&qru=/ta/sql-advanced/question-ranking&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D240)

# 思路
1. create index；
2. unique;
3. fulltext index;

# solution

## create index
```sql
create index idx_duration on examination_info(duration);
create unique index uniq_idx_exam_id on examination_info(exam_id);
create fulltext index full_idx_tag on examination_info(tag);
```