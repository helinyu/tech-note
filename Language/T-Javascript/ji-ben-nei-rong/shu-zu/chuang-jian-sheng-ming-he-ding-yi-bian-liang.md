# 创建—（声明和定义变量）

## **一、使用数组字面量**

这是最常见和简洁的创建数组的方式。

```javascript
let arr1 = []; // 创建一个空数组
let arr2 = [1, 2, 3]; // 创建一个包含具体元素的数组
let arr3 = [1, 'two', true]; // 可以包含不同类型的元素
```

## **二、使用`Array`构造函数**

1. 创建空数组：

```javascript
let arr4 = new Array();
```

2. 创建指定长度的空数组：

```javascript
let arr5 = new Array(5); // 创建一个长度为 5 的空数组，每个元素初始值为 undefined
```

3. 创建包含特定元素的数组：

```javascript
let arr6 = new Array(1, 2, 3);
```



4\. 使用 `Array.of()` 创建数组

`Array.of()` 创建包含指定元素的数组，与 `Array()` 不同的是，它不会因单一数值参数创建一个长度的空数组，而是直接创建带有该数值的数组。

```javascript
javascript复制代码let arr = Array.of(3); // 创建包含一个元素 3 的数组
console.log(arr); // 输出: [3]
```

#### 5. 使用 `Array.from()` 创建数组

`（1）Array.from()` 可以根据类数组对象或可迭代对象（如字符串、Set）创建数组。还可以传入回调函数生成数组元素。

```javascript
javascript复制代码let str = "hello";
let arrFromStr = Array.from(str); // 将字符串转换为字符数组
console.log(arrFromStr); // 输出: ['h', 'e', 'l', 'l', 'o']

let arrFromRange = Array.from({ length: 5 }, (_, i) => i * 2); // 创建 [0, 2, 4, 6, 8]
console.log(arrFromRange); // 输出: [0, 2, 4, 6, 8]
```



（2）使用`arguments`对象：在函数内部，`arguments`是一个类似数组的对象，可以通过以下方式转换为真正的数组：

```javascript
function myFunction() {
  let argsArray = Array.from(arguments);
  return argsArray;
}

let result = myFunction(1, 2, 3);
console.log(result); // [1, 2, 3]
```

#### 6. 创建空数组并动态添加元素

你可以先创建一个空数组，然后使用 `push()` 方法动态添加元素。

```javascript
javascript复制代码let arr = [];
arr.push(1);
arr.push(2);
console.log(arr); // 输出: [1, 2]
```



## **三、数组推导式（ES6 及更高版本）**

类似其他语言中的列表推导式，可以简洁地创建数组。

```javascript
let numbers = [1, 2, 3, 4, 5];
let doubledNumbers = [n * 2 for (n of numbers)];
console.log(doubledNumbers); // [2, 4, 6, 8, 10]
```



## 四、在 TypeScript 中创建数组

在 TypeScript 中，数组的创建除了与 JavaScript 相同外，还可以为数组定义元素的类型，以提高类型安全性。

**1 使用类型注解定义数组**

可以通过在类型后加上 `[]` 或使用 `Array<type>` 的方式来定义类型数组。

```typescript
let numArray: number[] = [1, 2, 3]; // 数字类型的数组
let strArray: string[] = ["apple", "banana"]; // 字符串类型的数组

// 使用泛型创建数组
let numArrayGeneric: Array<number> = [1, 2, 3];
let strArrayGeneric: Array<string> = ["apple", "banana"];
```

**6.2 使用联合类型创建混合数组**

TypeScript 允许创建包含多种类型元素的数组，可以使用联合类型来实现。

```typescript
let mixedArray: (number | string)[] = [1, "hello", 2, "world"];
```

**6.3 创建元组（Tuple）**

元组是 TypeScript 提供的一种特殊数组类型，允许你定义具有固定长度和类型的数组。

```typescript
let person: [string, number]; // 声明一个元组，包含字符串和数字
person = ["Alice", 25]; // 初始化元组
// person = [25, "Alice"]; // 错误: 类型不匹配
```

**6.4 多维数组**

多维数组是数组的数组，可以在 TypeScript 和 JavaScript 中轻松创建。

```typescript
let twoDArray: number[][] = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
];
```

#### 7. 数组的创建方式对比

| 方法                  | 描述                                         | 适用性                                              |
| ------------------- | ------------------------------------------ | ------------------------------------------------ |
| **数组字面量**           | 使用 `[]` 直接创建并初始化数组，简单快捷。                   | 最常用的方式，适用于大部分场景。                                 |
| **`Array()`**       | 使用 `Array()` 构造函数创建数组，既可以创建空数组，也可以同时初始化数组。 | 适用于需要创建指定长度的空数组或直接初始化数组的场景。                      |
| **`Array.of()`**    | 用于创建包含指定元素的数组，不会出现 `Array()` 的长度问题。        | 更可靠地创建数组，特别是当参数是单个数值时。                           |
| **`Array.from()`**  | 根据类数组或可迭代对象创建数组，可以通过回调函数生成数组元素。            | 适用于需要从类似数组对象（如字符串、Set、Map）生成数组的场景，或通过回调函数生成数组内容。 |
| **TypeScript 类型注解** | 为数组指定类型，使其类型更加安全。                          | 适用于类型严格的场景，避免类型错误。                               |
| **元组 (Tuple)**      | 定义固定长度和类型的数组。                              | 适用于需要对数组元素进行严格类型控制，并保证其顺序和长度的场景。                 |
| **多维数组**            | 定义数组的数组，可以表示矩阵、网格等复杂结构。                    | 适用于需要表达多维数据的场景。                                  |
