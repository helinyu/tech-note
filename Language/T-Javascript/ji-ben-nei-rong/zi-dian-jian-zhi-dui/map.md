# Map

`Map`是一种用于存储键值对的数据结构。

**特点：**

1. 键可以是任何类型的值，包括对象、函数、基本类型等。
2. 保持插入顺序，即遍历`Map`时按照插入的顺序返回键值对。
3. 提供了一些方便的方法来操作键值对，如`set`（设置键值对）、`get`（获取值）、`has`（检查键是否存在）、`delete`（删除键值对）等。

**用法：**

1.  创建一个新的`Map`：

    ```typescript
    const myMap = new Map();
    ```

**属性：**

* `size`：返回 `Map` 对象中键值对的数量。

**方法：**

&#x20;**\* new  创建**

* `set(key, value)`：设置键值对。将指定的键与值关联起来，并返回更新后的 `Map` 对象。
* `get(key)`：通过键获取对应的值。如果键不存在，则返回 `undefined`。
* `has(key)`：检查 `Map` 对象中是否存在指定的键，返回一个布尔值。
* `delete(key)`：删除指定键及其关联的值。如果键存在并成功删除，则返回 `true`；否则返回 `false`。
* `clear()`：移除 `Map` 对象中的所有键值对。
* `keys()`：返回一个新的可迭代对象，包含 `Map` 对象中所有的键。
* `values()`：返回一个新的可迭代对象，包含 `Map` 对象中所有的值。
* `entries()`：返回一个新的可迭代对象，包含 `Map` 对象中所有的键值对，形式为 `[key, value]` 的数组。
* `forEach(callbackFn[, thisArg])`：对 `Map` 对象中的每个键值对执行指定的回调函数。回调函数接受三个参数：值、键和 `Map` 对象本身。可以提供一个可选的 `thisArg` 参数来指定回调函数中 `this` 的值。 for.of

例如：

```typescript
const myMap = new Map(); // 创建
myMap.set('name', 'John');
myMap.set('age', 30);

console.log(myMap.size); // 2

console.log(myMap.get('name')); // John
console.log(myMap.has('age')); // true

myMap.delete('age');
console.log(myMap.has('age')); // false

const keys = myMap.keys();
for (const key of keys) {
  console.log(key);
}

const values = myMap.values();
for (const value of values) {
  console.log(value);
}

const entries = myMap.entries();
for (const [key, value] of entries) {
  console.log(`${key}: ${value}`);
}

myMap.forEach((value, key) => {
  console.log(`${key}: ${value}`);
});

//也可以使用forEach方法遍历：
myMap.forEach((value, key) => {
  console.log(`Key: ${key}, Value: ${value}`);
});

myMap.clear();
console.log(myMap.size); // 0
```
