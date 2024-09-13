# 排序

* **`sort()`**: 对数组进行排序（默认按照字符串 Unicode 编码排序，需要传递比较函数进行数字排序）

<mark style="color:red;">**ts/js中没有sorted方法**</mark>

```js
let arr = [3, 1, 4, 2, 5];
arr.sort((a, b) => a - b); // [1, 2, 3, 4, 5]
```
