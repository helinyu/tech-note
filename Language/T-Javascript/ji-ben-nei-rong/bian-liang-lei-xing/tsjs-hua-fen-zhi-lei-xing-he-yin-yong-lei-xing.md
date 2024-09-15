# TS/JS 划分值类型和引用类型

在 TypeScript 和 JavaScript 中，通常可以这样划分值类型和引用类型：

**值类型（原始类型）**：

*   `number`：数字类型是值类型，赋值时会进行值的复制。例如：

    ```javascript
    let a = 10;
    let b = a;
    a = 20;
    console.log(b); // 10，说明 b 不受 a 重新赋值的影响，是值类型的特点。
    ```
* `string`：字符串也是值类型，操作类似数字类型。
* `boolean`：布尔值同样是值类型。
* `null` 和 `undefined`：这两个特殊的值类型，赋值时也是值的复制。

**引用类型**：

*   `object`：对象是引用类型。当一个对象被赋值给另一个变量时，实际上是复制了引用地址，两个变量指向同一个内存中的对象。例如：

    ```javascript
    let obj1 = { name: 'John' };
    let obj2 = obj1;
    obj1.name = 'Mike';
    console.log(obj2.name); // 'Mike'，说明修改 obj1 会影响 obj2，因为它们指向同一个对象，是引用类型的特点。
    ```
* `array`：数组是引用类型，操作方式与对象类似。
* `function`：函数也是引用类型，赋值时复制的是函数的引用。

需要注意的是，在 JavaScript 和 TypeScript 中这种值类型和引用类型的区分并不像一些其他语言（如 C++、Java 等）那样严格，这是因为 JavaScript 和 TypeScript 的变量存储和操作方式有其独特性。
