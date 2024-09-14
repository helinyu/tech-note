# 创建

在 JavaScript 中，函数可以通过以下两种主要方式进行声明和定义：

## **一、函数声明（Function Declaration）**

1.  语法：

    ```javascript
    function functionName(parameters) {
      // 函数体
      return result;
    }
    ```
2.  特点：

    * 函数声明会在代码执行前被提升（hoisted）到其所在作用域的顶部。这意味着可以在函数声明之前调用该函数。
    * 例如：

    ```javascript
    foo(); // 可以正常调用，因为函数声明被提升了

    function foo() {
      console.log('Hello from foo!');
    }
    ```

## **二、函数表达式（Function Expression）**

1.  语法：

    ```javascript
    const functionName = function(parameters) {
      // 函数体
      return result;
    };
    ```

    或者使用箭头函数的形式：

    ```javascript
    const functionName = (parameters) => {
      // 函数体
      return result;
    };
    ```
2.  特点：

    * 函数表达式是在代码执行过程中，当遇到这个表达式时才被创建。因此，在函数表达式定义之前不能调用该函数。#&#x20;
    * 例如：

    ```javascript
    bar(); // 会报错，因为函数表达式在这一行之后才被定义
    const bar = function() {
      console.log('Hello from bar!');
    };
    ```

## **三、立即调用函数表达式（Immediately Invoked Function Expression - IIFE）**

1.  语法：

    ```javascript
    (function(parameters) {
      // 函数体
    })(arguments);
    ```

    或者使用箭头函数：

    ```javascript
    ((parameters) => {
      // 函数体
    })(arguments);
    ```
2.  特点：

    * 立即执行函数表达式在定义后立即被调用。<mark style="color:orange;">通常用于创建局部作用域，避免污染全局作用域</mark>。
    * 例如：

    ```javascript
    (function() {
      console.log('This is an IIFE.');
    })();
    ```
