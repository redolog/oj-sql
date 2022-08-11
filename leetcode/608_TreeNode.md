# 题目

[608. 树节点](https://leetcode.cn/problems/tree-node/)

# 思路
1. 使用switchcase语句分离每种情况；
2. 使用union组装每种情况；
3. 使用if判断分离每种情况；

# solution

## case when
```sql
SELECT
    id,
    CASE
        WHEN p_id is null THEN 'Root'
        WHEN id in (select distinct p_id from tree) THEN 'Inner'
        ELSE 'Leaf'
        END AS `type`
FROM tree;
```
## union where
```sql

SELECT id,'Root' AS 'type' FROM tree WHERE p_id IS NULL
UNION
SELECT id,'Inner' AS 'type'  FROM tree WHERE id IN (SELECT DISTINCT p_id FROM tree WHERE p_id IS NOT NULL) AND p_id IS NOT NULL
UNION
SELECT id,'Leaf' AS 'type'  FROM tree WHERE id NOT IN (SELECT DISTINCT p_id FROM tree WHERE p_id IS NOT NULL) AND p_id IS NOT NULL;

```
## if isnull where
```sql
# ifnull 三元运算符
SELECT
    id,
    IF(ISNULL(p_id),'Root',
       IF(id IN (SELECT p_id FROM tree), 'Inner','Leaf')) AS 'type'
FROM tree;
```