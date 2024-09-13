# 遍历

数组 + [遍历](../bian-li/)

## 1. **遍历数组**

* **`for` 循环**
* **`forEach()`**: 对数组的每个元素执行一次提供的函数
* **`map()`**: 对数组的每个元素调用函数，返回一个新数组

```js
let arr = [1, 2, 3];

// for 循环
for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
}

// forEach 遍历
arr.forEach((item) => {
  console.log(item);
});

// map 遍历
let newArr = arr.map((item) => item * 2); // [2, 4, 6]
```



## **2、过滤数组**

* **`filter()`**: 根据条件过滤数组，返回符合条件的元素组成的新数组

```js
js复制代码let arr = [1, 2, 3, 4, 5];
let filteredArr = arr.filter(item => item > 3); // [4, 5]
```
