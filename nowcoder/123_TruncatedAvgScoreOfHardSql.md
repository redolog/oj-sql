# 题目

[SQL123 SQL类别高难度试卷得分的截断平均值](https://www.nowcoder.com/practice/a690f76a718242fd80757115d305be45?tpId=240&tqId=2180959&ru=/exam/oj&qru=/ta/sql-advanced/question-ranking&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D240)

# 思路
1. 直接聚合函数算；
2. 也可以利用窗口函数排行，取出增序降序下除了倒一第一的分数数据；

# solution

## sum max min count round
直接算，截断平均数=(总数-最大分数-最小分数 )/(总数量-2) 。
小数保留一位。使用round。
```sql
select
    e.tag,
    e.difficulty,
    round((sum(score)-min(score)-max(score))/(count(score)-2),1) clip_avg_score
from exam_record r
join examination_info e
on (r.exam_id = e.exam_id)
where e.tag='SQL' and difficulty='hard';
```

## dense_rank
```sql
select
    tag,
    difficulty,
    round(avg(score),1) as clip_avg_score
from (
    select 
           exam_id, 
           tag, 
           difficulty, 
           score,
           dense_rank() over(order by score) as rank_asc,
           dense_rank() over(order by score desc) as rank_desc
    from exam_record 
    left join examination_info i 
    using(exam_id)
    where difficulty = 'hard' and tag = 'sql' and score is not null
) t_tmp
-- 去掉正数第一、倒数第一
where rank_asc != 1 and rank_desc != 1
group by tag;
```