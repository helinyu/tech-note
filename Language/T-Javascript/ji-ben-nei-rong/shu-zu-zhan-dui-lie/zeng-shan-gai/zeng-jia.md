# 增加

## 1、增加元素

### 1.1、基本使用方法

* **`push()`**: 在数组末尾添加元素
* **`unshift()`**: 在数组开头添加元素

```js
let arr = [1, 2, 3];

// 添加元素
arr.push(4); // [1, 2, 3, 4]
arr.unshift(0); // [0, 1, 2, 3, 4]
```

### 1.2、数组中插入数值/子数组

**方法一：使用`splice`方法**

`splice`方法可以在数组中指定位置添加或删除元素。

```javascript
const arr = [1, 2, 3, 4];
// 在索引为 2 的位置插入值为 5 的元素
arr.splice(2, 0, 5);
console.log(arr); // [1, 2, 5, 3, 4]
```

**方法二：使用展开运算符**

```javascript
const arr = [1, 2, 3, 4];
// 在索引为 2 的位置插入值为 5 的元素
const newArr = [...arr.slice(0, 2), 5,...arr.slice(2)];
console.log(newArr); // [1, 2, 5, 3, 4]
```











