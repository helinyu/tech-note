# README

脚本语言的规范



ES7（ECMAScript 2016）和ES6（ECMAScript 2015）是JavaScript语言的两个版本更新。ES6是JavaScript的一次重大更新，而ES7则是相对较小的更新。下面是两者的主要差别：

#### 1. **ES6 (ECMAScript 2015)** — 主要功能

ES6是JavaScript的一次非常重要的更新，带来了大量新特性，极大地扩展了语言的功能。以下是一些重要的新功能：

* **let 和 const**：用于声明变量，`let` 有块作用域，`const` 声明常量。
* **箭头函数**：简洁的函数语法，并且绑定上下文的 `this`。
* **类（class）**：引入了基于类的面向对象编程语法。
* **模块（modules）**：支持 `import` 和 `export` 语法，模块化开发。
* **模板字符串**：使用反引号 (\`) 来定义字符串，支持嵌入表达式。
* **解构赋值**：从数组或对象中提取值，赋值给变量。
* **Promise**：用于处理异步操作的更优雅的方式。
* **默认参数**：函数参数可以有默认值。
* **Rest 参数和扩展运算符**：`...` 用于函数参数和数组/对象的拷贝和合并。
* **生成器函数**：通过 `function*` 语法定义生成器，用于迭代。

#### 2. **ES7 (ECMAScript 2016)** — 主要功能

ES7相对于ES6的变化较小，只引入了两个主要新特性：

*   **Array.prototype.includes()**：用于检查数组是否包含某个值，返回 `true` 或 `false`。它比 `indexOf()` 更直观，例如：

    ```javascript
    let arr = [1, 2, 3];
    arr.includes(2);  // true
    arr.includes(4);  // false
    ```
*   **指数运算符（**）\*\*：简化了幂运算的表达，例如：

    ```javascript
    let result = 2 ** 3;  // 8，相当于Math.pow(2, 3)
    ```

#### 总结

* **ES6** 是一次大规模的更新，添加了很多新特性，极大地增强了JavaScript语言的功能。
* **ES7** 则是一次较小的更新，主要引入了 `Array.prototype.includes()` 和指数运算符 `**`。

因此，ES7和ES6的主要差别在于更新的规模和引入的新特性数量。
