# 集合set

在 TypeScript/JavaScript 中，`Set` 提供了一些内置的属性和方法，用于操作集合。以下是 `Set` 的主要属性和方法：

#### 1. 属性

**1.1. `size`**

`size` 返回集合中元素的数量。

```typescript
const mySet = new Set([1, 2, 3]);
console.log(mySet.size); // 3
```

#### 2. 方法

**2.1. `add(value)`**

向集合中添加指定的元素。如果该元素已经存在，则不会重复添加。

```typescript
mySet.add(4);
mySet.add(3); // 不会添加重复的元素
```

**2.2. `delete(value)`**

从集合中删除指定的元素，返回 `true` 表示成功删除，`false` 表示该元素不存在。

```typescript
console.log(mySet.delete(2)); // true
console.log(mySet.delete(5)); // false
```

**2.3. `has(value)`**

检查集合中是否存在指定的元素，返回 `true` 或 `false`。

```typescript
console.log(mySet.has(3)); // true
console.log(mySet.has(5)); // false
```

**2.4. `clear()`**

移除集合中的所有元素。

```typescript
mySet.clear();
console.log(mySet.size); // 0
```

**2.5. `forEach(callbackFn)`**

对集合中的每个元素执行指定的回调函数。

```typescript
mySet.add(1);
mySet.add(2);
mySet.forEach((value) => {
    console.log(value);
});
// 输出: 1 2
```

**2.6. `keys()`**

返回一个包含集合中所有元素的迭代器，迭代器的值与集合中的元素相同。

```typescript
const keysIterator = mySet.keys();
console.log(keysIterator.next().value); // 1
```

**2.7. `values()`**

返回一个包含集合中所有元素的迭代器。与 `keys()` 方法行为相同，`Set` 的键和值相同。

```typescript
const valuesIterator = mySet.values();
console.log(valuesIterator.next().value); // 1
```

**2.8. `entries()`**

返回一个新的迭代器对象，其中每个元素是一个包含键和值相同的数组 `[value, value]`。

```typescript
const entriesIterator = mySet.entries();
console.log(entriesIterator.next().value); // [1, 1]
```

**2.9. `Symbol.iterator`**

`Set` 也是可迭代对象，所以可以使用 `for...of` 循环遍历集合的元素。

```typescript
for (const value of mySet) {
    console.log(value); // 输出集合中的每个值
}
```

#### 总结

| 属性/方法             | 描述                                    |
| ----------------- | ------------------------------------- |
| `size`            | 返回集合中的元素数量。                           |
| `add(value)`      | 添加一个元素到集合中。                           |
| `delete(value)`   | 删除集合中的指定元素。                           |
| `has(value)`      | 检查集合中是否包含某个元素。                        |
| `clear()`         | 清空集合中的所有元素。                           |
| `forEach(fn)`     | 遍历集合中的所有元素，执行回调函数。                    |
| `keys()`          | 返回集合中所有元素的迭代器（键和值相同）。                 |
| `values()`        | 返回集合中所有元素的迭代器（与 `keys()` 相同）。         |
| `entries()`       | 返回集合中所有元素的迭代器，元素为 `[value, value]` 对。 |
| `Symbol.iterator` | 使 `Set` 可用于 `for...of` 循环。            |

#### 使用 `Set` 的典型场景

* 去重：例如从数组中去掉重复的值。
* 查找唯一元素：存储只需要一次的元素。
* 记录访问过的项：比如处理缓存或者跟踪状态。
