# while

## `while` 和 `do...while` 循环

### **1 `while` 循环**

`while` 循环根据条件执行代码块，适合不确定循环次数的场景。

```javascript
let i = 0;
let arr = [10, 20, 30];
while (i < arr.length) {
    console.log(arr[i]); // 输出: 10, 20, 30
    i++;
}
```

### **2 `do...while` 循环**

`do...while` 循环至少执行一次，然后再检查条件。

```javascript
let i = 0;
let arr = [10, 20, 30];
do {
    console.log(arr[i]); // 输出: 10, 20, 30
    i++;
} while (i < arr.length);
```
