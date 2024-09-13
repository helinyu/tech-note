# unorderedmap、multiMap、unordered\_multimap?

在 JavaScript 中，`Map` 是一种键值对的集合，和普通对象类似，但它保留了插入顺序。JavaScript 原生并不提供类似于 C++ 中的 `unordered_map`、`multimap` 或 `unordered_multimap` 的集合类型，不过可以通过其他方式实现类似的功能。

## 1. **Map**

* JavaScript 的 `Map` 是有序的，并且根据插入的顺序来遍历键值对。
* 同一个键只能对应一个值，所以它不支持多个相同的键。

```js
let map = new Map();
map.set('key1', 'value1');
map.set('key2', 'value2');
```

## 2. **Unordered Map（无序的 Map）**

* JavaScript 中没有专门的 `unordered_map` 类型。
* 如果你不关心插入顺序，可以使用普通的 `Object`，因为它在某些情况下表现得无序，但从 ECMAScript 2015 开始，`Object` 的键遍历顺序也变得有规律了。
* 或者你可以通过自定义数据结构或使用库（如 `Immutable.js`）实现无序的行为。

```js
let obj = { key1: 'value1', key2: 'value2' }; // 对象的键值对存储无序
```

## 3. **Multimap（多重映射）**

* JavaScript 原生不支持 `multimap`，即同一个键可以映射到多个值。
* 你可以使用 `Map`，并让每个键映射到一个数组来实现类似的功能。

```js
let multimap = new Map();
multimap.set('key1', ['value1', 'value2']);
multimap.get('key1').push('value3');
```

## 4. **Unordered Multimap（无序多重映射）**

* JavaScript 中也没有类似于 C++ 的 `unordered_multimap`。
* 如果不需要键的有序性，仍然可以通过对象 (`Object`) 和数组的组合来实现多个值的映射，并且不关心插入顺序。

```js
let unorderedMultimap = {
    key1: ['value1', 'value2'],
    key2: ['value3', 'value4']
};
unorderedMultimap['key1'].push('value5');
```

如果你需要更复杂的数据结构，可能需要引入一些第三方库，比如 `lodash`、`Immutable.js`，或者手动实现你所需的行为。

