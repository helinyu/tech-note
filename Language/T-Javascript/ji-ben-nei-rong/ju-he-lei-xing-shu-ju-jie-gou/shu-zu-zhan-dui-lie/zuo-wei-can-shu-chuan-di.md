# 作为参数传递

#### 传递的是数组的引用，所以是可以知道大小的，不用像C语言那样还要传长度



**TypeScript 示例：**

```typescript
function printArray(arr: number[]) {
  for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
  }
}

const numbers: number[] = [1, 2, 3, 4, 5];
printArray(numbers);
```

**JavaScript 示例：**

```javascript
function printArray(arr) {
  for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
  }
}

const numbers = [1, 2, 3, 4, 5];
printArray(numbers);
```

在这两种语言中，当数组作为参数传递给函数时，实际上是传递了数组的引用。这意味着函数内部对数组的修改会影响到原始数组。如果不想影响原始数组，可以在函数内部创建一个数组的副本进行操作。

例如：

```javascript
function modifyArray(arr) {
  // 创建一个副本
  const newArr = [...arr];
  newArr.push(6);
  return newArr;
}

const numbers = [1, 2, 3, 4, 5];
const modifiedNumbers = modifyArray(numbers);
console.log(numbers); // [1, 2, 3, 4, 5]
console.log(modifiedNumbers); // [1, 2, 3, 4, 5, 6]
```

```typescript
function modifyArray(arr: number[]): number[] {
  // 创建一个副本
  const newArr = [...arr];
  newArr.push(6);
  return newArr;
}

const numbers: number[] = [1, 2, 3, 4, 5];
const modifiedNumbers = modifyArray(numbers);
console.log(numbers); // [1, 2, 3, 4, 5]
console.log(modifiedNumbers); // [1, 2, 3, 4, 5, 6]
```
