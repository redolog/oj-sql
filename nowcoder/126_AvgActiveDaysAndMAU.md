# 题目

[SQL126 平均活跃天数和月活人数](https://www.nowcoder.com/practice/9e2fb674b58b4f60ac765b7a37dde1b9?tpId=240&tqId=2183005&ru=/exam/oj&qru=/ta/sql-advanced/question-ranking&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D240)

# 思路
1. 提取年月：
   1. EXTRACT(YEAR_MONTH From submit_time)
   2. date_format(submit_time, '%Y%m')
2. 提取年月日：
   1. date_format(submit_time,'%Y%m%d')
3. 计数去重：
   1. count(distinct col1, col2)

# solution

## extract year_month date_format count distinct
```sql
select
    EXTRACT(YEAR_MONTH From submit_time) month,
    round(count(distinct uid,date_format(submit_time,'%Y%m%d'))/count(distinct uid),2) avg_active_days,
    count(distinct uid) mau
from exam_record
where submit_time is not null and year(submit_time)=2021
group by EXTRACT(YEAR_MONTH From submit_time)
;
```