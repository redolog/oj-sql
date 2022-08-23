# 题目

[SQL129 月均完成试卷数不小于3的用户爱作答的类别](https://www.nowcoder.com/practice/b1d13efcfa0c4ecea517afbdb9090845?tpId=240&tqId=2183022&ru=/exam/oj&qru=/ta/sql-advanced/question-ranking&sourceUrl=%2Fexam%2Foj%3Fpage%3D1%26tab%3DSQL%25E7%25AF%2587%26topicId%3D240)

# 思路
1. 先找月均提交试卷数达到3的用户id；
2. 根据uid条件筛选，输出tag数据即可；


# solution

## group by count having dateformat
```sql
with report as(
    select
        date_format(submit_time,'%Y%m') month,
        uid,
        count(submit_time) cnt
    from exam_record
    where submit_time is not null
    group by month,uid
    having cnt>=3
)

select
    info.tag,
    count(tag) tag_cnt
from exam_record re
join examination_info info
on (re.exam_id=info.exam_id)
where uid in (
    select uid from report
)
group by info.tag
order by tag_cnt desc;
```