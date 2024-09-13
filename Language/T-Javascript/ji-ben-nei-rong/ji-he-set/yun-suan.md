# 运算

在 TypeScript/JavaScript 中，`Set` 本身并没有内置提供集合运算的专用方法，如并集、交集和差集等。不过，我们可以通过使用 JavaScript 的原生方法和一些自定义逻辑来实现这些集合运算。以下是一些常见的 `Set` 运算及其实现方式：

#### 1. 并集（Union）

并集是将两个集合的所有元素合并，去除重复的元素。

**实现方式：**

可以使用 `Set` 的构造函数与展开运算符（`...`）来实现。

```typescript
const setA = new Set([1, 2, 3]);
const setB = new Set([3, 4, 5]);

const union = new Set([...setA, ...setB]);
console.log(union); // 输出: Set { 1, 2, 3, 4, 5 }
```

#### 2. 交集（Intersection）

交集是两个集合的共同元素。

**实现方式：**

可以使用 `Set.prototype.has()` 方法来过滤两个集合中的公共元素。

```typescript
const intersection = new Set([...setA].filter(x => setB.has(x)));
console.log(intersection); // 输出: Set { 3 }
```

#### 3. 差集（Difference）

差集是一个集合中的元素减去另一个集合中的元素，即保留只存在于第一个集合中的元素。

**实现方式：**

可以使用 `Set.prototype.has()` 过滤只存在于第一个集合中的元素。

```typescript
const difference = new Set([...setA].filter(x => !setB.has(x)));
console.log(difference); // 输出: Set { 1, 2 }
```

#### 4. 对称差（Symmetric Difference）

对称差是只存在于两个集合之一中的元素，排除两个集合共有的元素。

**实现方式：**

可以结合两次差集运算来实现。

```typescript
const symmetricDifference = new Set([...setA].filter(x => !setB.has(x)).concat([...setB].filter(x => !setA.has(x))));
console.log(symmetricDifference); // 输出: Set { 1, 2, 4, 5 }
```

#### 5. 子集（Subset）

子集是指集合 A 中的所有元素都存在于集合 B 中。

**实现方式：**

可以使用 `every()` 方法来检查是否所有元素都存在。

```typescript
const isSubset = [...setA].every(x => setB.has(x));
console.log(isSubset); // 输出: false
```

#### 6. 超集（Superset）

超集是指集合 A 包含集合 B 中的所有元素。

**实现方式：**

与子集类似，可以通过检查集合 B 的所有元素是否都在集合 A 中。

```typescript
const isSuperset = [...setB].every(x => setA.has(x));
console.log(isSuperset); // 输出: false
```

#### 7. 例子汇总

```typescript
const setA = new Set([1, 2, 3]);
const setB = new Set([3, 4, 5]);

// 并集
const union = new Set([...setA, ...setB]);
console.log('Union:', union); // Set { 1, 2, 3, 4, 5 }

// 交集
const intersection = new Set([...setA].filter(x => setB.has(x)));
console.log('Intersection:', intersection); // Set { 3 }

// 差集
const difference = new Set([...setA].filter(x => !setB.has(x)));
console.log('Difference:', difference); // Set { 1, 2 }

// 对称差
const symmetricDifference = new Set([...setA].filter(x => !setB.has(x)).concat([...setB].filter(x => !setA.has(x))));
console.log('Symmetric Difference:', symmetricDifference); // Set { 1, 2, 4, 5 }

// 子集
const isSubset = [...setA].every(x => setB.has(x));
console.log('Is A subset of B:', isSubset); // false

// 超集
const isSuperset = [...setB].every(x => setA.has(x));
console.log('Is A superset of B:', isSuperset); // false
```

#### 总结

尽管 TypeScript/JavaScript 中的 `Set` 没有内置的集合运算方法，但是通过组合使用 `Set` 的基本 API 和一些函数方法（如 `filter`、`every`）可以轻松实现常见的集合运算。
