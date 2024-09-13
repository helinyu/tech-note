# 声明和定义变量和常量

在 JavaScript 和 TypeScript 中，声明和定义变量与常量有几种不同的方式。下面将详细介绍 `var`、`let`、`const` 三种关键字的用法及其区别。

## `1、var`

`var` 是 JavaScript 中最早用于声明变量的关键字，它具有函数作用域（Function Scope）和变量提升（Hoisting）的特性。

**示例代码**

```javascript
function example() {
    var x = 10;
    if (true) {
        var x = 20; // 同一个变量
        console.log(x); // 20
    }
    console.log(x); // 20
}

example();
```

**特性**

* **函数作用域**：变量在函数内声明，无论在函数的哪个部分声明，变量在函数整个生命周期内都是可见的。
* **变量提升**：变量声明会被提升到函数或全局作用域的顶部，但赋值不会提升。

## `2、let`

`let` 是 ES6 引入的，用于声明变量。它具有块级作用域（Block Scope），并且不会被提升。

**示例代码**

```javascript
function example() {
    let x = 10;
    if (true) {
        let x = 20; // 不同的变量
        console.log(x); // 20
    }
    console.log(x); // 10
}

example();
```

**特性**

* **块级作用域**：变量只在声明的块（例如 `{}` 内）中可见。
* **不会提升**：声明的变量不会被提升到块或函数的顶部。

## `3、const`

`const` 也是 ES6 引入的，用于声明常量。它具有块级作用域，并且声明时必须初始化，且一旦初始化后不能再更改。

**示例代码**

```javascript
function example() {
    const x = 10;
    // x = 20; // 错误：常量不能重新赋值

    // 对于对象和数组，引用不可变，但内容可变
    const obj = { key: "value" };
    obj.key = "newValue"; // 合法：修改对象的属性
    console.log(obj); // { key: "newValue" }

    const arr = [1, 2, 3];
    arr.push(4); // 合法：修改数组的内容
    console.log(arr); // [1, 2, 3, 4]
}

example();
```

**特性**

* **块级作用域**：常量只在声明的块（例如 `{}` 内）中可见。
* **不可变引用**：声明时必须初始化，且不能重新赋值。但对于对象和数组，其属性和元素可以修改。

#### 变量和常量的区别

1. **`var`**：
   * 函数作用域。
   * 变量提升。
   * 可以重新声明和赋值。
2. **`let`**：
   * 块级作用域。
   * 不会提升。
   * 不能重新声明，但可以重新赋值。
3. **`const`**：
   * 块级作用域。
   * 不会提升。
   * 不能重新声明，也不能重新赋值。
   * 对于对象和数组，其引用不可变，但内容可变。



## 4、TypeScript

在 TypeScript 中，变量和常量的声明与 JavaScript 基本一致，但增加了类型注解，使得代码更安全和可读。

**示例代码**

```typescript
let x: number = 10;
const y: string = "hello";

let obj: { key: string } = { key: "value" };
obj.key = "newValue"; // 合法

let arr: number[] = [1, 2, 3];
arr.push(4); // 合法
```

**特性**

* **类型注解**：可以在变量和常量声明时指定类型，从而在编译时进行类型检查。
*   **静态类型检查**：可以在编写代码时提前发现潜在的错误。

    ####

## 5、使用建议

* **`var`**：尽量避免使用，建议用 `let` 和 `const` 替代。
* **`let`**：用于声明可以被重新赋值的变量，具有块级作用域。
* **`const`**：用于声明不会被重新赋值的常量或对象，尽量多使用 `const`，以避免不必要的赋值错误。



## 6、 区别总结

| 特性    | `var`               | `let`         | `const`       |
| ----- | ------------------- | ------------- | ------------- |
| 作用域   | 函数作用域或全局作用域         | 块级作用域         | 块级作用域         |
| 变量提升  | 是（初始化为 `undefined`） | 是（但有暂时性死区）——否 | 是（但有暂时性死区）——否 |
| 可重新声明 | 是                   | 否             | 否             |
| 可重新赋值 | 是                   | 是             | 否             |