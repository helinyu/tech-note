# symbol

`Symbol`是一种基本数据类型，用于创建唯一的标识符。

**特点：**

1. **唯一性**：每个通过 `Symbol()` 创建的符号都是唯一的，即使它们具有相同的描述。
2. **不可枚举性**：默认情况下，使用 `Symbol` 创建的属性不会出现在 `for...in` 循环或 `Object.keys()` 等常规的对象枚举方法中。

**用法：**

1.  创建符号：

    ```typescript
    const symbol1 = Symbol();
    const symbol2 = Symbol('description');
    ```

    可以为符号提供一个描述性的字符串，但这仅用于调试目的，不会影响符号的唯一性。
2.  作为对象属性：

    ```typescript
    const obj = {
      [symbol1]: 'value1',
      [symbol2]: 'value2'
    };
    ```
3.  内置符号： JavaScript 中有一些内置的符号，可以用于特定的目的。例如，`Symbol.iterator` 用于定义对象的迭代行为。

    ```typescript
    const arr = [1, 2, 3];
    const iterator = arr[Symbol.iterator]();
    console.log(iterator.next()); // { value: 1, done: false }
    ```
4.  共享符号： 通过 `Symbol.for(key)` 可以创建或获取一个全局共享的符号。如果具有相同 `key` 的符号已经存在，它将返回那个已有的符号；否则，它会创建一个新的符号并注册到全局符号注册表中。

    ```typescript
    const sharedSymbol1 = Symbol.for('sharedSymbol');
    const sharedSymbol2 = Symbol.for('sharedSymbol');
    console.log(sharedSymbol1 === sharedSymbol2); // true
    ```

所以，Symbol.for('sharedSymbol') 和Symbol('sharedSymbol') 是有差别的。

```
Symbol.for('sharedSymbol') 返回的是同一个
Symbol('sharedSymbol') 不同的一个
```
