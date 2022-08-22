# ANY_VALUE(arg) 函数

[MySQL官方 ANY_VALUE(arg)](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_any-value)

# 背景
牛客使用了最新版本的MySQL，开启了` ONLY_FULL_GROUP_BY` 模式，如果在SELECT中的列，没有在GROUP BY中出现，那么这个SQL是不合法的，直接拒绝执行。

使用 `ANY_VALUE` 可以抑制这种拒绝。SQL可以正常执行。

## 举例
- [127_MonthCntAndAvgDayCnt](../nowcoder/127_MonthCntAndAvgDayCnt.md)