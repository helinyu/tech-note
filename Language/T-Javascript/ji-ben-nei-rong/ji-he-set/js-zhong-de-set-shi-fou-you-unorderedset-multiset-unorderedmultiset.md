# js中的set是否有unorderedSet multiSet unordered\_multiSet?

在 JavaScript 中，`Set` 是一种用于存储**唯一值**的数据结构。和 `Map` 类似，JavaScript 并不提供像 C++ 中的 `unordered_set`、`multiset` 或 `unordered_multiset` 这样的集合类型。不过可以通过某些技巧和第三方库来实现类似的功能。

#### 1. **Set**

* JavaScript 的 `Set` 是有序的，它保留了插入元素的顺序。
* `Set` 中的值是唯一的，不能有重复的元素。

```js
let set = new Set();
set.add(1);
set.add(2);
set.add(2);  // 2 已存在，无法添加重复值
```

#### 2. **Unordered Set（无序集合）**

* JavaScript 中没有专门的 `unordered_set` 类型。
* 如果你不关心元素的插入顺序，可以使用普通的对象 (`Object`)，对象的键是无序的（虽然现代 JavaScript 的对象键遍历有一定顺序，但它不保证顺序性）。

```js
let unorderedSet = {1: true, 2: true};
```

#### 3. **Multiset（多重集合）**

* JavaScript 原生不支持 `multiset`，即可以存储重复值的集合。
* 可以使用 `Map` 或 `Object`，将元素作为键，出现的次数作为值来模拟 `multiset` 的行为。

```js
let multiset = new Map();
multiset.set(1, (multiset.get(1) || 0) + 1);  // 添加元素 1
multiset.set(2, (multiset.get(2) || 0) + 1);  // 添加元素 2
multiset.set(1, (multiset.get(1) || 0) + 1);  // 再次添加元素 1
console.log(multiset.get(1));  // 输出 2，表示元素 1 出现了两次
```

#### 4. **Unordered Multiset（无序多重集合）**

* JavaScript 中也没有直接的 `unordered_multiset` 实现。
* 如果不关心元素的插入顺序，同样可以使用对象 (`Object`) 来记录每个元素的出现次数。

```js
let unorderedMultiset = {};
unorderedMultiset[1] = (unorderedMultiset[1] || 0) + 1;
unorderedMultiset[2] = (unorderedMultiset[2] || 0) + 1;
unorderedMultiset[1] = (unorderedMultiset[1] || 0) + 1;
console.log(unorderedMultiset[1]);  // 输出 2，表示元素 1 出现了两次
```

#### 总结：

* **Unordered Set**: 可以使用 `Object` 实现，但不保证完全无序。
* **Multiset**: 可以使用 `Map` 或 `Object` 来记录元素和它们的出现次数。
* **Unordered Multiset**: 同样可以通过 `Object` 模拟。

对于更复杂的集合操作，第三方库（如 `lodash` 或 `Immutable.js`）可能会提供更简便的解决方案。
