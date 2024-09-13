# 切片slice

`slice()`方法用于从已有数组中返回选定的元素。

**语法**：

`array.slice(start, end)`

* `start`：可选。规定从何处开始选取。如果是负数，那么它规定从数组尾部开始算起的位置。如果未指定，`slice()`会从索引 0 开始。
* `end`：可选。规定从何处结束选取。该参数是数组片断结束处的数组下标。如果没有指定该参数，那么切分的数组包含从`start`到数组结束的所有元素。如果这个参数是负数，那么它规定的是从数组尾部开始算起的元素。

**示例**：

```javascript
const arr = [1, 2, 3, 4, 5];

// 从索引 1 开始到索引 3（不包括索引 3）
const slicedArr1 = arr.slice(1, 3);
console.log(slicedArr1); // [2, 3]

// 从索引 2 开始到数组末尾
const slicedArr2 = arr.slice(2);
console.log(slicedArr2); // [3, 4, 5]

// 使用负数索引，从倒数第三个元素开始到数组末尾
const slicedArr3 = arr.slice(-3);
console.log(slicedArr3); // [3, 4, 5]
```
