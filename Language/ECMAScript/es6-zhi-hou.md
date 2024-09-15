# ES6之后

ES6是JavaScript语言的一次重大更新，而从ES7（ECMAScript 2016）到ES14的每一版本都在逐步增强和优化语言的功能。

#### 1. **ES7（2016）**:

* **Array.prototype.includes()**：用于检测数组中是否存在某个值。
* **指数运算符（**）\*\*：使用 `**` 进行幂运算。 相当于pow&#x20;

#### 2. **ES8（2017）**:

* **Async/Await**：基于 `Promise` 的异步处理，简化了异步代码的书写和逻辑结构。
* **Object.entries()** 和 **Object.values()**：返回对象的键值对和属性值的数组。
* **字符串填充**：`String.prototype.padStart()` 和 `String.prototype.padEnd()` 用于在字符串的开始或末尾添加指定字符。
* **Object.getOwnPropertyDescriptors()**：返回对象所有自身属性的描述符。

#### 3. **ES9（2018）**:

*   **Rest/Spread 属性**：扩展了对象解构和合并的能力，例如：

    ```javascript
    let {a, ...rest} = {a: 1, b: 2, c: 3}; // rest 为 {b: 2, c: 3}
    ```
* **异步迭代器**：通过 `for await...of` 进行异步迭代。
* **Promise.finally()**：在 `Promise` 的 `then` 或 `catch` 之后无论如何都会执行的回调。

#### 4. **ES10（2019）**:

* **Array.prototype.flat()** 和 **Array.prototype.flatMap()**：用于展平多维数组。
* **Object.fromEntries()**：从键值对创建对象。
* **字符串的 trimStart() 和 trimEnd()**：用于去除字符串开头或结尾的空格。

#### 5. **ES11（2020）**:

* **可选链操作符（?.）**：简化对深层嵌套对象属性的访问，避免空值错误。
* **空值合并操作符（??）**：用于处理 `null` 或 `undefined` 值时提供默认值。
* **Promise.allSettled()**：等待所有 `Promise` 完成（无论成功或失败）。
* **BigInt**：用于表示和操作超大整数。

#### 6. **ES12（2021）**:

* **逻辑赋值运算符**：`&&=`, `||=`, `??=`，简化了常见的赋值操作。
* **String.prototype.replaceAll()**：替换字符串中所有匹配的子字符串。
* **WeakRef**：用于创建对对象的弱引用。
* **私有字段（Private Fields）**：通过 `#` 定义类的私有属性。

#### 7. **ES13（2022）**:

* **顶级 await**：允许在模块的顶级作用域中使用 `await`，使异步代码更灵活。
* **类的静态块**：提供了一种机制，可以在类中定义静态代码块以初始化类级别的内容。
* **增强的正则表达式匹配**：改进了捕获组和匹配机制。

#### 8. **ES14（2023）** — ECMAScript 2023：

* **Array.prototype.toSorted()**：返回排序后的数组副本，不修改原数组。
* **Array.prototype.toReversed()**：返回反转后的数组副本，不修改原数组。
* **Array.prototype.toSpliced()**：生成一个数组的副本，并执行指定的替换操作。
* **Array.prototype.with()**：返回一个新的数组，其中指定索引处的值被替换，而不会修改原数组。
* **Hashbang (`#!`) 支持**：允许在 JavaScript 文件的第一行使用 `#!` 来指定脚本解释器（常见于 Node.js）。
* **Symbol.prototype.description**：提供直接访问 `Symbol` 的描述的方式。
* **WeakMap.prototype.emplace()**：通过一个更新函数处理映射中的键值对，简化了存在性检查和插入操作。

#### 总结

相对于ES6，ES14（2023）为JavaScript引入了更现代化、更简洁的编程模式，特别是针对数组和异步操作的增强。自ES6以来，每一个新版本都为开发者提供了更强大的工具和优化，极大地提高了代码的可读性、性能和可维护性。
