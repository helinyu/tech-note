# 闭包

**闭包（Closure）是指一个函数能够访问其外部函数作用域中的变量，即使外部函数已经执行完毕。**

## **一、闭包的基本概念**

### **1.形成闭包的条件**：

* 存在一个内部函数（嵌套函数）。
* 内部函数引用了外部函数的变量。
* 外部函数将内部函数作为**返回值返回**或者**在外部作用域中被引用**。

### **2.示例**：

```javascript
function outerFunction() {
  const outerVariable = 'I am an outer variable';
  function innerFunction() {
    console.log(outerVariable);
  }
  return innerFunction;
}

const innerFunc = outerFunction();
innerFunc(); // 输出：I am an outer variable
```

在这个例子中，`innerFunction`就是一个闭包，它可以访问外部函数`outerFunction`中的变量`outerVariable`，即使`outerFunction`已经执行完毕。

## **二、闭包的作用**

### **1. 实现数据封装和隐藏**：

* 通过闭包，可以创建私有变量，这些变量只能在闭包内部被访问，外部无法直接修改。
* 示例：

```javascript
function createCounter() {
  let count = 0;
  return function() {
    return ++count;
  };
}

const counter = createCounter();
console.log(counter()); // 1
console.log(counter()); // 2
```

在这个例子中，<mark style="color:orange;">变量</mark><mark style="color:orange;">`count`</mark><mark style="color:orange;">是私有的，只能通过返回的内部函数来访问和修改</mark>。

### **2. 模拟块级作用域**：

* 在 JavaScript 中，没有传统编程语言中的块级作用域。但可以使用闭包来模拟块级作用域，确保变量在特定的代码块执行完毕后被正确清理。
* 示例：

```javascript
{
  let blockVariable = 'I am a block variable';
  console.log(blockVariable);
}
// console.log(blockVariable); // 报错，因为 blockVariable 在外部不可访问

function createBlock() {
  let blockVariable = 'I am a block variable in closure';
  return function() {
    console.log(blockVariable);
  };
}

const blockFunc = createBlock();
blockFunc(); // 输出：I am a block variable in closure
```

### **3. 函数柯里化（Currying）**：

* 闭包可以用于实现函数柯里化，<mark style="color:orange;">**将一个多参数的函数转换为一系列单参数的函数**</mark>。
* 示例：

```javascript
function add(a) {
  return function(b) {
    return a + b;
  };
}

const addFive = add(5);
console.log(addFive(3)); // 8
```

## **三、闭包的注意事项**



### **1、 内存管理**：

* 由于闭包会保留对外部变量的引用，可能会导致内存泄漏。如果闭包中引用的外部变量不再被需要，应该及时将其设置为`null`或其他适当的值，以便垃圾回收器回收内存。



### **2、 变量的生命周期**：

* 闭包中的变量的生命周期会延长，直到没有任何引用指向包含它们的闭包为止。这可能会导致一些意外的行为，特别是在循环中使用闭包时。
* 示例：

```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(function() {
    console.log(i);
  }, 1000);
}
// 输出：3, 3, 3（而不是期望的 0, 1, 2）

for (let j = 0; j < 3; j++) {
  setTimeout(function() {
    console.log(j);
  }, 1000);
}
// 输出：0, 1, 2
```

在第一个例子中，由于使用了`var`声明变量`i`，在循环结束后，`i`的值为`3`。并且在每个`setTimeout`的回调函数中，它们都引用了同一个变量`i`，所以最终输出都是`3`。而在第二个例子中，使用了`let`声明变量`j`，每个循环迭代都会创建一个新的变量`j`，因此每个回调函数都能正确地输出对应的`j`的值。
