# Prototype原型

在 JavaScript 中，`prototype`（原型）是一个非常重要的概念。

**一、概述**

<mark style="color:red;">**每个函数都有一个**</mark><mark style="color:red;">**`prototype`**</mark><mark style="color:red;">**属性，它是一个对象（称为原型对象）**</mark>。当使用构造函数创建对象实例时，这些实例可以通过原型链访问到构造函数的原型对象上的属性和方法。

**二、作用**

1. **方法共享**：
   * 如前面提到的，将方法定义在构造函数的`prototype`属性上，可以让多个实例共享这些方法，节省内存。
   *   例如：

       ```javascript
       function Person(name, age) {
         this.name = name;
         this.age = age;
       }
       Person.prototype.sayHello = function() {
         console.log(`Hello, I am ${this.name}.`);
       };
       const person1 = new Person('Alice', 30);
       const person2 = new Person('Bob', 25);
       person1.sayHello(); // Hello, I am Alice.
       person2.sayHello(); // Hello, I am Bob.
       ```
   * 这里`person1`和`person2`都可以调用`sayHello`方法，而这个方法只在内存中存在一份，存储在`Person`的原型对象上。
2. **实现继承**：
   * 通过原型链可以实现一种类似继承的机制。一个构造函数的原型对象可以是另一个构造函数的实例，从而实现属性和方法的继承。
   *   例如：

       ```javascript
       function Animal() {
         this.isAlive = true;
       }
       Animal.prototype.move = function() {
         console.log('Moving...');
       };
       function Dog() {
         this.breed = 'Golden Retriever';
       }
       Dog.prototype = new Animal();
       Dog.prototype.bark = function() {
         console.log('Woof!');
       };
       const myDog = new Dog();
       console.log(myDog.isAlive); // true
       myDog.move(); // Moving...
       myDog.bark(); // Woof!
       ```
   * 这里`Dog`的实例`myDog`通过原型链继承了`Animal`的属性和方法，同时又有自己的`breed`属性和`bark`方法。

**三、原型链查找机制**

当访问一个对象的属性或方法时，JavaScript 引擎首先在对象本身查找。如果没有找到，就会沿着原型链向上查找，直到找到该属性或方法或者到达原型链的顶端（`Object.prototype`）。

例如：

```javascript
function Person(name) {
  this.name = name;
}
Person.prototype.sayHello = function() {
  console.log(`Hello, I am ${this.name}.`);
};
const person = new Person('Alice');
person.sayHello();
```

当调用`person.sayHello()`时，首先在`person`对象本身查找`sayHello`方法，没有找到后就沿着原型链在`Person.prototype`上找到并调用该方法。
