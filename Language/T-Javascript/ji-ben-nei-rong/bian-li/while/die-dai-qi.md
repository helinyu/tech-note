# 迭代器

**迭代器的基本原理：**

* 通过 `.next()` 方法遍历集合，每次调用返回一个对象 `{ value: x, done: true/false }`，其中 `value` 是当前的值，`done` 表示是否迭代结束。

**生成迭代器的示例：**

```js
const arr = [1, 2, 3];
const iterator = arr[Symbol.iterator]();

console.log(iterator.next()); // { value: 1, done: false }
console.log(iterator.next()); // { value: 2, done: false }
console.log(iterator.next()); // { value: 3, done: false }
console.log(iterator.next()); // { value: undefined, done: true }
```

常见的是和while一起结合使用的。



{% hint style="info" %}
迭代器

迭代器是根据不同的数据结构而有所不同的。 从上面的内容可看出来，迭代器是数组的迭代器，是线性的，所以next()指的就是下一个。可能还有其他数据结构，迭代器也会不一样。
{% endhint %}



