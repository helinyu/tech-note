# 对象创建

在 JavaScript 中，可以使用以下几种方式定义对象：

## **一、对象字面量**

这是最常见和简洁的定义对象的方式。

```javascript
let obj = {
  property1: value1,
  property2: value2,
  method: function() {
    // 方法体
  }
};
```

例如：

```javascript
let person = {
  name: 'Alice',
  age: 30,
  sayHello: function() {
    console.log(`Hello, I am ${this.name}.`);
  }
};
```

## **二、使用构造函数**

通过定义构造函数来创建对象。构造函数通常以大写字母开头，用于初始化对象的属性。

```javascript
function Person(name, age) {
  this.name = name;
  this.age = age;
  this.sayHello = function() {
    console.log(`Hello, I am ${this.name}.`);
  };
}

let person1 = new Person('Bob', 25);
```

## **三、使用 Object.create() 方法**

`Object.create()`方法可以创建一个新对象，并指定该对象的原型。

```javascript
let prototype = {
  sayHello: function() {
    console.log(`Hello from prototype.`);
  }
};

let obj = Object.create(prototype);
obj.name = 'Charlie';
obj.age = 35;
```

在这个例子中，`obj`对象的原型是`prototype`，它继承了`prototype`对象的`sayHello`方法。

## **四、使用 ES6 的类定义对象**

如前面提到过的，ES6 引入了类的语法糖，可以使用类来定义对象。

```javascript
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  sayHello() {
    console.log(`Hello, I am ${this.name}.`);
  }
}

let person2 = new Person('David', 40);
```
