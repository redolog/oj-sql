# CASE WHEN  语句

## 例子
根据一个例子即可掌握sql中的switchcase语句：
```sql
SELECT OrderID, Quantity,
CASE
    WHEN Quantity > 30 THEN "The quantity is greater than 30"
    WHEN Quantity = 30 THEN "The quantity is 30"
    ELSE "The quantity is under 30"
END
FROM OrderDetails;
```

等价于if语句：
```sql
SELECT
    id,
    IF(ISNULL(p_id),'Root',
       IF(id IN (SELECT p_id FROM tree), 'Inner','Leaf')) AS 'type'
FROM tree;
```