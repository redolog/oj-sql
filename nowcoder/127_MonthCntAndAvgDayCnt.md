# 题目

[SQL127 月总刷题数和日均刷题数](https://www.nowcoder.com/practice/f6b4770f453d4163acc419e3d19e6746?tpId=240&tqId=2183006&ru=/exam/oj&qru=/ta/sql-advanced/question-ranking&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D240)

# 思路
1. ANY_VALUE：
   1. 抑制 ONLY_FULL_GROUP_BY 模式下，select选出了groupby中未包含的字段下不执行的问题。
2. 提取年月日：
   1. date_format(submit_time,'%Y%m%d')
3. 获取日期对应月天数
   1. day(LAST_DAY(submit_time))
4. 合并结果集：
   1. union all 不需要去重
5. group by with rollup
   1. 可对groupby之后第一个字段进行汇总


# solution

## anyvalue day lastday unionall
```sql
select
   date_format(submit_time, '%Y%m') submit_month,
   any_value(count(question_id)) month_q_cnt,
   any_value(
           round(count(question_id) / day(LAST_DAY(submit_time)), 3)
      ) avg_day_q_cnt
from
   practice_record
where
   date_format(submit_time, '%Y') = '2021'
group by
   submit_month
-- 不需要去重
union all
select
   '2021汇总' as submit_month,
   count(*) as month_q_cnt,
   round(count(*) / 31, 3) as avg_day_q_cnt
from
   practice_record
where
      score is not null
      and year(submit_time) = '2021'
order by
   submit_month;
```

## group by with rollup
分组汇总，可以考虑`with rollup`，跟在`group by`之后的第一个字段将被汇总。

取 `day(LAST_DAY(submit_time))` 之后再使用聚合函数，是因为数据有多条，我们只取一条，同理使用`avg`也可以。

```sql
select any_value(coalesce (DATE_FORMAT(submit_time, '%Y%m'),"2021汇总")) submit_month,
       any_value(count(submit_time)) month_q_cnt,
       any_value(round(count(question_id)/MAX(day(LAST_DAY(submit_time))), 3)) avg_day_q_cnt
from practice_record
where YEAR(submit_time)='2021'
group by DATE_FORMAT(submit_time, "%Y%m") -- 这里不能用别名
with rollup ;

```
这里的`coalesce`可以用`ifnull`替代。
```sql
select any_value(ifnull (DATE_FORMAT(submit_time, '%Y%m'),"2021汇总")) submit_month,
       any_value(count(submit_time)) month_q_cnt,
       any_value(round(count(question_id)/MAX(day(LAST_DAY(submit_time))), 3)) avg_day_q_cnt
from practice_record
where YEAR(submit_time)='2021'
group by DATE_FORMAT(submit_time, "%Y%m") -- 这里不能用别名
with rollup ;
```