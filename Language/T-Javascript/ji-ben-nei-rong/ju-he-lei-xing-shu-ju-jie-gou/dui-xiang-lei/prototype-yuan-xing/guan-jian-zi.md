# 关键字

在 JavaScript 中，与原型相关的主要关键字有以下几个：

### `1、prototype`：

* 每个函数都有一个`prototype`属性，用于指向一个对象，这个对象被称为该函数的原型对象。通过原型对象，可以为使用该函数作为构造函数创建的对象实例定义共享的属性和方法。
*   例如：

    ```javascript
    function Person() {}
    Person.prototype.name = 'Anonymous';
    const person1 = new Person();
    const person2 = new Person();
    console.log(person1.name); // 'Anonymous'
    console.log(person2.name); // 'Anonymous'
    ```

### `2、__proto__`：

* 这是一个非标准的属性（在现代 JavaScript 中不建议直接使用），它存在于对象实例上，用于指向创建该实例的构造函数的原型对象。它实际上是原型链查找的内部实现机制。
*   例如：

    ```javascript
    function Person() {}
    const person = new Person();
    console.log(person.__proto__ === Person.prototype); // true
    ```

### `3、constructor`：

* 存在于原型对象上的属性，指向创建该原型对象的构造函数。
*   例如：

    ```javascript
    function Person() {}
    console.log(Person.prototype.constructor === Person); // true
    ```
