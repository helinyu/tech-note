# 最值

<mark style="color:red;">**常见的使用方法就是基础库提供的max和min。**</mark>



**一、使用排序**

1.  获取最大值：

    ```javascript
    const arr = [5, 3, 8, 1, 6];
    arr.sort((a, b) => b - a);
    const maxValue = arr[0];
    console.log(maxValue); // 8
    ```
2.  获取最小值：

    ```javascript
    const arr = [5, 3, 8, 1, 6];
    arr.sort((a, b) => a - b);
    const minValue = arr[0];
    console.log(minValue); // 1
    ```

**二、使用扩展运算符和`Math`方法**

1.  获取最大值：

    ```javascript
    const arr = [5, 3, 8, 1, 6];
    const maxValue = Math.max(...arr);
    console.log(maxValue); // 8
    ```
2.  获取最小值：

    ```javascript
    const arr = [5, 3, 8, 1, 6];
    const minValue = Math.min(...arr);
    console.log(minValue); // 1
    ```

**三、遍历数组**

1.  获取最大值：

    ```javascript
    const arr = [5, 3, 8, 1, 6];
    let max = arr[0];
    for (let i = 1; i < arr.length; i++) {
      if (arr[i] > max) {
        max = arr[i];
      }
    }
    console.log(max); // 8
    ```
2.  获取最小值：

    ```javascript
    const arr = [5, 3, 8, 1, 6];
    let min = arr[0];
    for (let i = 1; i < arr.length; i++) {
      if (arr[i] < min) {
        min = arr[i];
      }
    }
    console.log(min); // 1
    ```
