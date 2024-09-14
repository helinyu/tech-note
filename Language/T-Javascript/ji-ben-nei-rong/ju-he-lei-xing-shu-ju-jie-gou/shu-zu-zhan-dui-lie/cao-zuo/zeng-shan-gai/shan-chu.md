# 删除



### 2.1 基本方法

* **`pop()`**: 移除数组末尾的元素
* **`shift()`**: 移除数组开头的元素

```
let arr = [1, 2, 3];

// 删除元素
arr.pop(); // [0, 1, 2, 3]
arr.shift(); // [1, 2, 3]
```

### 2.2 **使用`splice`方法\[值、子数组]**

`splice`方法可以从数组中删除一个或多个元素。

```javascript
const arr = [1, 2, 3, 4, 5];
// 删除索引为 2 的元素
arr.splice(2, 1);
console.log(arr); // [1, 2, 4, 5]
```

### **2.3、使用`filter`方法**

`filter`方法创建一个新数组，包含通过提供函数实现的测试的所有元素。

```javascript
const arr = [1, 2, 3, 4, 5];
// 删除值为 3 的元素
const newArr = arr.filter(item => item!== 3);
console.log(newArr); // [1, 2, 4, 5]
```







