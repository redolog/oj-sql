# WindowFunction
# 窗口函数
- [MySQL官方文档：12.21.1 Window Function Descriptions](https://dev.mysql.com/doc/refman/8.0/en/window-function-descriptions.html)

非聚合的窗口函数，大意是针对一组数据，进行相邻的一些操作，如：

| 窗口函数 | 含义                                  |
| --- |-------------------------------------|
|  `CUME_DIST()`   | 累计分布值                               |
|  `ROW_NUMBER()`   | 分区内的序号                              |
|  `RANK()`   | 分区内的排名，排名间有缺口（同排名有多个值时，下一个排名按个数插入缺口 |
|   `DENSE_RANK()`   | 分区内的排名，排名间无缺口（前面有并列的情况，排名依然紧凑连续）    |
|  `PERCENT_RANK()`   | 排名百分比                               |
|  `NTILE()`   | 分区序号：属于第几个分区                        |
|  `NTH_VALUE()`   | 窗口内的第n个值                            |
|  `LEAD()`   | 分区内下一个值                             |
|  `LAG()`   | 分区内上一个值                             |
|  `LAST_VALUE()`   | 分区内最后一个值                            |
|  `FIRST_VALUE()`   | 分区内第一个值                             |

通过官方文档的示例，不难发现，这些函数在内部应该是做了`groupBy map`的操作，序列（窗口内）数据一般有序，根据有序的属性，自然可以处理各种排名问题。