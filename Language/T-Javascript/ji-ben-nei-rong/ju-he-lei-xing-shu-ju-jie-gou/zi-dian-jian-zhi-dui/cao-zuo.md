# 操作



**1. 检查键是否存在**

* 在对象中可以使用 `in` 操作符或 `hasOwnProperty` 方法。
* 在 `Map` 中可以使用 `has()` 方法。

```ts
ts复制代码let obj = { name: 'Alice', age: '25' };
console.log('age' in obj); // 输出：true
console.log(obj.hasOwnProperty('age')); // 输出：true

let map = new Map([['apple', 10]]);
console.log(map.has('apple')); // 输出：true
```

**2. 删除键值对**

* 在对象中可以使用 `delete` 操作符。
* 在 `Map` 中可以使用 `delete()` 方法。

```ts
// 删除对象中的键值对
delete obj['age'];

// 删除 Map 中的键值对
map.delete('apple');
```

**3. 清空字典**

* 清空对象可以直接将其设置为空对象 `{}`。
* `Map` 提供了 `clear()` 方法。

```ts
// 清空对象
obj = {};

// 清空 Map
map.clear();
```

#### 5. **强类型键值对 (TypeScript)**

在 TypeScript 中，可以为键值对结构定义更具体的类型，以确保类型安全。

**定义对象类型：**

```ts
interface Person {
  name: string;
  age: number;
}

let person: Person = {
  name: 'Alice',
  age: 25
};
```

**使用泛型定义 `Map` 类型：**

```ts
let map: Map<string, number> = new Map();
map.set('apple', 10);
map.set('banana', 20);
```
