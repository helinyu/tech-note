# 增删改

### <mark style="color:red;">`splice()`</mark><mark style="color:red;">方法用于对数组进行操作，可以实现添加、删除或替换数组中的元素。</mark>

**语法**：

`array.splice(start, deleteCount, item1, item2,...)`

* `start`：指定修改的开始位置（索引）。如果是负数，则从数组末尾开始计数。
* `deleteCount`：可选，表示要删除的元素个数。如果省略，则从`start`位置开始到数组末尾的所有元素都将被删除。
* `item1, item2,...`：可选，要添加到数组中的新元素。

**示例**：

1. 删除元素：

```javascript
let arr = [1, 2, 3, 4, 5];
arr.splice(2, 1); // 从索引 2 开始，删除 1 个元素
console.log(arr); // [1, 2, 4, 5]
```

2. 添加元素：

```javascript
let arr = [1, 2, 3];
arr.splice(1, 0, 1.5, 2.5); // 从索引 1 开始，删除 0 个元素，插入 1.5 和 2.5
console.log(arr); // [1, 1.5, 2.5, 2, 3]
```

3. 替换元素：

```javascript
let arr = [1, 2, 3, 4, 5];
arr.splice(2, 2, 2.5, 3.5); // 从索引 2 开始，删除 2 个元素，插入 2.5 和 3.5
console.log(arr); // [1, 2, 2.5, 3.5, 5]
```
