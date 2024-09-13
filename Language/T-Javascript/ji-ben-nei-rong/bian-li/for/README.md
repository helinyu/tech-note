# for

在 TypeScript 和 JavaScript 中，循环遍历是处理数组和对象的常见操作。常用的循环方式有 `for`、`for...of`、`for...in`、`forEach()` 等，它们各自适用于不同的场景和数据结构。下面是每种循环遍历方式的详细介绍。

## 1. `for` 循环

`for` 循环是最基础的一种遍历方式，适用于数组和类数组对象。可以根据索引来访问数组的每个元素。

**语法：**

```javascript
for (let i = 0; i < array.length; i++) {
    // 操作 array[i]
}
```

**示例：**

```javascript
let arr = [10, 20, 30, 40];
for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]); // 输出: 10, 20, 30, 40
}
```

## 2. `for...of` 循环

`for...of` 是 ES6 引入的一种遍历方式，适用于数组、字符串、`Map`、`Set` 等可迭代对象。它会直接遍历每个值，而不是索引。

**语法：**

```javascript
for (let element of array) {
    // 操作 element
}
```

**示例：**

```javascript
let arr = [10, 20, 30, 40];
for (let value of arr) {
    console.log(value); // 输出: 10, 20, 30, 40
}
```

**适用场景：**

* 遍历数组元素时，不需要访问索引。
* 遍历字符串、`Set`、`Map` 等可迭代对象。

## 3. `for...in` 循环

`for...in` 用于遍历对象的**可枚举属性**或数组的索引（不是值）。它返回的是对象的键或数组的索引。

**语法：**

```javascript
for (let key in object) {
    // 操作 key 和 object[key]
}
```

**示例：**

遍历对象：

```javascript
let obj = { name: "Alice", age: 25, job: "developer" };
for (let key in obj) {
    console.log(`${key}: ${obj[key]}`);
}
// 输出:
// name: Alice
// age: 25
// job: developer
```

遍历数组（不推荐）：

```javascript
let arr = [10, 20, 30, 40];
for (let index in arr) {
    console.log(index, arr[index]); // 输出: 0 10, 1 20, 2 30, 3 40
}
```

> **注意**: `for...in` 不适合遍历数组，因为它遍历的是数组的**索引**，而不是值。如果数组中有继承的属性或方法，它们也会被枚举出来。

## 4. `forEach()` 方法

`forEach()` 是数组对象的内置方法，用于遍历数组中的每个元素，适合需要执行一次回调操作的场景。

**语法：**

```javascript
array.forEach((element, index, array) => {
    // 操作 element
});
```

**示例：**

```javascript
let arr = [10, 20, 30, 40];
arr.forEach((value, index) => {
    console.log(`Index: ${index}, Value: ${value}`);
});
// 输出:
// Index: 0, Value: 10
// Index: 1, Value: 20
// Index: 2, Value: 30
// Index: 3, Value: 40
```

**适用场景：**

* 不需要返回结果，只是对数组的每个元素执行操作。
