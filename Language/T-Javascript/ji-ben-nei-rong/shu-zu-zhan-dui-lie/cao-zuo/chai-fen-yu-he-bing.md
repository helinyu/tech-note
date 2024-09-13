# 拆分与合并

* **`slice()`**: 返回数组的一个子数组（不改变原数组）
* **`splice()`**: 添加、删除或替换数组中的元素（会修改原数组）

```js
let arr = [1, 2, 3, 4, 5];

// 截取子数组
let slicedArr = arr.slice(1, 3); // [2, 3]

// 删除和替换元素
arr.splice(2, 1); // [1, 2, 4, 5] 删除索引2处的1个元素
arr.splice(1, 2, 9, 10); // [1, 9, 10, 5] 从索引1处删除2个元素并插入9, 10
```


