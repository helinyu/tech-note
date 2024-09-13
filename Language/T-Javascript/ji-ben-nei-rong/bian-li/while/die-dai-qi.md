# 迭代器

**迭代器的基本原理：**

* 通过 `.next()` 方法遍历集合，每次调用返回一个对象 `{ value: x, done: true/false }`，其中 `value` 是当前的值，`done` 表示是否迭代结束。

**生成迭代器的示例：**

```js
js复制代码const arr = [1, 2, 3];
const iterator = arr[Symbol.iterator]();

console.log(iterator.next()); // { value: 1, done: false }
console.log(iterator.next()); // { value: 2, done: false }
console.log(iterator.next()); // { value: 3, done: false }
console.log(iterator.next()); // { value: undefined, done: true }
```

常见的是和while一起结合使用的。

