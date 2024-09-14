# 查找\[索引、元素、包含]

## 1、除去了遍历的方式查找



## 2、\[内置方法]**查找元素**

* **`indexOf()`**: 返回元素第一次出现的索引，如果不存在则返回 -1  —— <mark style="color:red;">索引</mark>
* **`includes()`**: 判断数组中是否包含某个元素 —— <mark style="color:red;">包含</mark>
* **`find()`**: 找到第一个符合条件的元素，返回该元素（如果不存在则返回 `undefined`） ——<mark style="color:red;">元素</mark>
* **`findIndex()`**: 找到第一个符合条件的元素，返回其索引（如果不存在则返回 `-1`） —— <mark style="color:red;">索引【判断条件】</mark>

```js
js复制代码let arr = [1, 2, 3, 4, 5];
console.log(arr.indexOf(3)); // 输出：2
console.log(arr.includes(6)); // 输出：false
let arr = [1, 2, 3, 4, 5];
let found = arr.find(item => item > 3); // 4
let foundIndex = arr.findIndex(item => item > 3); // 3
```

