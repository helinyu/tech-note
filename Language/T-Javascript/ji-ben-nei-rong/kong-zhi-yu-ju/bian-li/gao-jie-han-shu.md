# 高阶函数

## 1. `map()` 方法

`map()` 方法用于对数组的每个元素执行回调函数，并返回一个新的数组。适合需要转换数组元素的场景。

**语法：**

```javascript
let newArray = array.map((element, index, array) => {
    return element * 2; // 或者其他操作
});
```

**示例：**

```javascript
let arr = [1, 2, 3, 4];
let newArr = arr.map(value => value * 2);
console.log(newArr); // 输出: [2, 4, 6, 8]
```

**适用场景：**

* 需要在遍历过程中生成并返回新数组的情况。

## 2. 其他遍历方法

* **`reduce()`**：用于累积处理数组，适合需要将数组归约为单个值的情况。
* **`filter()`**：返回符合条件的元素数组。
* **`some()` 和 `every()`**：用于检查数组中是否有元素满足某个条件或是否所有元素都满足某个条件。
