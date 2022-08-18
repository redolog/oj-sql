# 题目

[SQL118 创建一张新表](https://www.nowcoder.com/practice/a61ee5519d14444aa99e530309a8e043?tpId=240&tqId=2223564&ru=/exam/oj&qru=/ta/sql-advanced/question-ranking&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D240)

# 思路
1. CREATE TABLE IF NOT EXISTS；

# solution

## CREATE TABLE IF NOT EXISTS
```sql
CREATE TABLE IF NOT EXISTS user_info_vip (
    id int PRIMARY KEY AUTO_INCREMENT COMMENT '自增ID',
    uid int UNIQUE NOT NULL COMMENT '用户ID',
    nick_name varchar(64) COMMENT '昵称',
    achievement int DEFAULT 0 COMMENT '成就值',
    `level` int COMMENT '用户等级',
    job varchar(32) COMMENT '职业方向',
    register_time datetime DEFAULT CURRENT_TIMESTAMP COMMENT '注册时间'
) 
COMMENT 'vip用户表' CHARACTER SET utf8 COLLATE utf8_general_ci;
```
