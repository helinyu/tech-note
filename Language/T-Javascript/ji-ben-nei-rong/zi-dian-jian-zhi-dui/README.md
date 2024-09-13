# 字典/键值对

字典（通常称为对象或 `Map`）是用来存储键值对的数据结构。JS 中的对象和 `Map` 都可以用作字典，但它们有不同的特性和使用场景。

#### 1. **使用对象（Object）作为字典**

对象是 JS 中最基本的字典形式。可以用对象的属性来存储键值对。

```ts
let dict: { [key: string]: string } = {
  name: 'Alice',
  age: '25',
  country: 'USA'
};

// 访问字典的值
console.log(dict['name']); // 输出：Alice
console.log(dict.age); // 输出：25

// 添加/更新键值对
dict['city'] = 'New York';
dict.country = 'Canada';

// 删除键值对
delete dict['age'];

console.log(dict); // 输出：{ name: 'Alice', country: 'Canada', city: 'New York' }
```

**特点：**

* 键是字符串或符号（Symbol）。
* 不能直接使用其他类型作为键（如数字、对象等，数字会被自动转换为字符串）。
* 无法跟踪插入顺序。

#### 2. **使用 `Map`**

`Map` 是 ES6 引入的，用于存储键值对，并且可以使用任意类型作为键。相比对象，`Map` 提供了更多的功能，如保留插入顺序和更好的性能。

```ts
let map = new Map<string, string>();

// 添加键值对
map.set('name', 'Bob');
map.set('age', '30');

// 访问键值对
console.log(map.get('name')); // 输出：Bob

// 删除键值对
map.delete('age');

// 判断键是否存在
console.log(map.has('age')); // 输出：false

// 获取 Map 的大小
console.log(map.size); // 输出：1

// 遍历 Map
map.forEach((value, key) => {
  console.log(key, value);
});
```

**特点：**

* 键可以是任意类型，如对象、字符串、数字等。
* `Map` 保留键值对的插入顺序。
* 提供了更多有用的 API（如 `set`、`get`、`delete`、`has`、`size` 等）。

#### 3. **数组中的键值对**

虽然数组本质上是一个有序列表，但可以将数组与键值对结合使用，尤其是在二维数组的情况下，常用于简单的键值对存储。

**二维数组存储键值对：**

```ts
let arr: [string, number][] = [
  ['apple', 10],
  ['banana', 20],
  ['orange', 30]
];

// 访问键值对
console.log(arr[0]); // 输出：['apple', 10]

// 遍历键值对
for (let [key, value] of arr) {
  console.log(`${key}: ${value}`);
}
```

**将数组转换为对象或 `Map`：**

* 使用 `Object.fromEntries()` 可以将键值对数组转换为对象。
* 使用 `new Map()` 可以将键值对数组转换为 `Map`。

```ts
ts复制代码let arr = [['apple', 10], ['banana', 20], ['orange', 30]];

// 转换为对象
let obj = Object.fromEntries(arr);
console.log(obj); // 输出：{ apple: 10, banana: 20, orange: 30 }

// 转换为 Map
let map = new Map(arr);
console.log(map); // 输出：Map(3) { 'apple' => 10, 'banana' => 20, 'orange' => 30 }
```

#### 3. **对象 vs `Map`**

| 特性   | Object            | Map                 |
| ---- | ----------------- | ------------------- |
| 键类型  | 字符串或 `Symbol`     | 任意类型（对象、数字、字符串等）    |
| 键的顺序 | 无明确顺序             | 按插入顺序               |
| 访问性能 | 适用于少量键值对          | 适用于大量键值对            |
| 常用操作 | 使用 `.` 或 `[]` 访问键 | 使用 `set` 和 `get` 操作 |
| 操作方法 | 没有直接的内置方法         | 提供多种操作方法            |
| 大小计算 | 需要手动计算            | 使用 `size` 属性        |

#### 4. **遍历字典**

**遍历对象：**

可以使用 `for...in` 循环遍历对象的键，或者使用 `Object.keys()`、`Object.values()`、`Object.entries()` 方法。

```ts
let obj = { name: 'Alice', age: 25, city: 'New York' };

// 使用 for...in 遍历键
for (let key in obj) {
  console.log(key, obj[key]);
}

// 使用 Object.keys(), Object.values(), Object.entries()
console.log(Object.keys(obj)); // ['name', 'age', 'city']
console.log(Object.values(obj)); // ['Alice', 25, 'New York']
console.log(Object.entries(obj)); // [['name', 'Alice'], ['age', 25], ['city', 'New York']]
```

**遍历 `Map`：**

`Map` 提供了直接的遍历方法，如 `forEach()` 和 `for...of`。

```ts
let map = new Map([
  ['name', 'Alice'],
  ['age', '25'],
  ['city', 'New York']
]);

// 使用 forEach 遍历
map.forEach((value, key) => {
  console.log(key, value);
});

// 使用 for...of 遍历
for (let [key, value] of map) {
  console.log(key, value);
}
```

#### 5. **对象与 `Map` 的互相转换**

**对象转换为 `Map`：**

可以使用 `Object.entries()` 方法获取对象的键值对，然后将其传入 `Map` 构造函数。

```ts
let obj = { name: 'Alice', age: '25' };
let map = new Map(Object.entries(obj));
console.log(map); // 输出：Map(2) { 'name' => 'Alice', 'age' => '25' }
```

**`Map` 转换为对象：**

可以使用 `Array.from()` 将 `Map` 转换为键值对数组，然后用 `Object.fromEntries()` 进行转换。

```ts
let map = new Map([['name', 'Alice'], ['age', '25']]);
let obj = Object.fromEntries(map);
console.log(obj); // 输出：{ name: 'Alice', age: '25' }
```

#### 总结：

* **对象 (Object)**：适合处理简单的键值对，键必须为字符串或 `Symbol`。
* **`Map`**：适合存储大量键值对，键可以是任意类型，并且保留插入顺序。
* **数组键值对**：二维数组可以用于简单的键值对存储，并且可以通过 `Object.fromEntries()` 或 `new Map()` 进行转换。

如果你的场景需要复杂的键（如对象）或需要频繁的查找和插入操作，`Map` 是一个更好的选择。如果只需要简单的键值对，`Object` 已经足够。
