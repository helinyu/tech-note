# 索引区间indices

如果说索引区间，可以理解为从一个起始索引到一个结束索引之间的范围。\
例如，对于数组 `const arr = [1, 2, 3, 4, 5];`：\


* 索引区间 `[0, 2]` 表示从索引 0 开始到索引 2（不包括索引 2），即包含元素 `1` 和 `2`。
* 索引区间 `[2, arr.length]`（假设 `arr.length` 是数组长度）表示从索引 2 开始到数组末尾，即包含元素 `3`、`4` 和 `5`。

\
在一些操作中，比如 `slice()`、`splice()`等方法可以使用索引区间来指定操作的范围。
