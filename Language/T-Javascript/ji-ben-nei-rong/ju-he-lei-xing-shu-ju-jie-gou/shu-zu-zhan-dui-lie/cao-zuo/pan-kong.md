# 判空

<mark style="color:red;">**没有内置的判空方法**</mark>



在 TypeScript 和 JavaScript 中，可以通过以下几种方式判断数组是否为空：

1.  使用 `length` 属性：

    ```javascript
    const arr = [];
    if (arr.length === 0) {
      console.log('数组为空');
    } else {
      console.log('数组不为空');
    }
    ```
2.  使用 `Array.isArray` 和 `length`：

    ```javascript
    const arr = [];
    if (Array.isArray(arr) && arr.length === 0) {
      console.log('数组为空');
    } else {
      console.log('数组不为空');
    }
    ```
3.  使用 `Array.prototype.every`：

    ```javascript
    const arr = [];
    const isEmpty = arr.every(item =>!item);
    if (isEmpty) {
      console.log('数组为空');
    } else {
      console.log('数组不为空');
    }
    ```
4.  使用 `Object.keys`（不推荐，因为可能会有一些边缘情况）：

    ```javascript
    const arr = [];
    if (Object.keys(arr).length === 0) {
      console.log('数组为空');
    } else {
      console.log('数组不为空');
    }
    ```
