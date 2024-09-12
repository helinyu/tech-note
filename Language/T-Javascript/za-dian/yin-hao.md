# 引号

在 JavaScript 中，**没有三对双引号**这样的语法。JavaScript 使用以下三种方式来定义字符串：

1. **单引号** (`'`)
2. **双引号** (`"`)
3. **反引号** (`` ` ``)，用于模板字符串

#### 1. 单引号和双引号

单引号和双引号在 JavaScript 中功能相同，定义的字符串没有区别，只是两种不同的表示方法，主要区别在于使用时需要配对。如果字符串内包含了引号，可以使用另一种引号来避免转义。

```javascript
let singleQuoteString = 'Hello, World!';
let doubleQuoteString = "Hello, World!";

// 如果需要在字符串中包含引号
let quoteInSingle = 'She said, "Hello"';
let quoteInDouble = "It's a sunny day";
```

#### 2. 反引号（模板字符串）

反引号是 ES6（ECMAScript 2015）引入的，用来创建模板字符串。模板字符串可以跨多行，也允许嵌入变量和表达式，使用 `${}` 语法来进行变量插值。

```javascript
let name = "Alice";
let templateString = `Hello, ${name}!`;  // 输出 "Hello, Alice!"

// 多行字符串
let multiLineString = `This is a
multi-line
string.`;
console.log(multiLineString);
```

#### 三对双引号

像 Python 中的三对引号（`"""`）那样的多行字符串表示法在 JavaScript 中是没有的。要实现多行字符串和插值，使用反引号（模板字符串）是最佳选择。

```javascript
let multiLine = `This is a multi-line
string in JavaScript using backticks.`;
console.log(multiLine);
```

总结：JavaScript 没有三对双引号的语法，通常使用反引号（模板字符串）来实现多行字符串和变量插值。



{% hint style="info" %}
小结：

1、js中单引号和双引号没有差别，主要是为了配对，用另外一种引号来避免当前引号的转义

2、js中没有三对引号，【python、swift中都有三对引号可以实现多行】， js中使用了反引号通过模板实现多行，同时可以插值


{% endhint %}

