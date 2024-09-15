# 变量类型

在 TypeScript 和 JavaScript 中，变量主要有以下几种类型：

**一、原始类型（Primitive Types）**

1. `number`：用于表示数字，包括整数和浮点数。
   * 例如：`let num: number = 42;`
   * 或者在 JavaScript 中不声明类型直接赋值：`let num = 42;`
2. `string`：表示文本字符串。
   * 例如：`let str: string = "Hello World";`
   * JavaScript 中：`let str = "Hello World";`
3. `boolean`：表示布尔值，即 `true` 或 `false`。
   * 例如：`let isTrue: boolean = true;`
   * JavaScript 中：`let isTrue = true;`
4. `null` 和 `undefined`：
   * `null` 表示一个空值或者不存在的对象引用。
   * `undefined` 表示未初始化的值或者不存在的变量。

**二、对象类型（Object Types）**

1. `object`：在 TypeScript 和 JavaScript 中，几乎所有不是原始类型的值都是对象。对象可以包含属性和方法。
   * 例如：`let obj: object = { name: "John", age: 30 };`
   * JavaScript 中：`let obj = { name: "John", age: 30 };`
2. `Array`：表示数组，可以存储一组相同类型或不同类型的值。
   * 例如：`let arr: number[] = [1, 2, 3];`（TypeScript）或者 `let arr = [1, 2, 3];`（JavaScript）。
   * 也可以使用泛型的方式表示数组类型：`let arr: Array<number> = [1, 2, 3];`（TypeScript）。
3. `Function`：表示函数类型。
   * 例如：`let func: (a: number, b: number) => number = (a, b) => a + b;`（TypeScript）。
   * JavaScript 中函数可以直接定义和赋值给变量：`let func = function(a, b) { return a + b; };`

**三、特殊类型**

1. `any`：在 TypeScript 中，`any` 类型表示可以是任何类型的值。使用 `any` 类型会失去类型检查的好处。
   * 例如：`let value: any = 42;` `value = "Hello";` `value = true;`
2. `unknown`：也表示可以是任何类型的值，但比 `any` 更安全，因为在对 `unknown` 类型的值进行操作之前必须进行类型检查。
   * 例如：`let value: unknown = 42;`
   * 如果要使用这个值，需要进行类型检查：`if (typeof value === "number") { console.log(value + 10); }`
3. `void`：通常用于表示没有返回值的函数类型。
   * 例如：`let func: () => void = () => { console.log("This function returns nothing."); }`（TypeScript）。
   * JavaScript 中：`function func() { console.log("This function returns nothing."); }`。
4. `never`：表示永远不会有返回值的函数类型，或者表示一个不会正常结束的类型。
   * 例如：`function error(message: string): never { throw new Error(message); }`（TypeScript）。
