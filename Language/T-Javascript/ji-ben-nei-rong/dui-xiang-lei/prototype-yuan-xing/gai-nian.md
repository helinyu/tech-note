# 概念

在 JavaScript 中，原型链是实现继承的一种机制。

**一、基本概念**

每个对象都有一个指向其原型对象的内部链接，这个链接被称为`[[Prototype]]`（在一些浏览器中通过`__proto__`访问，但这是一个非标准属性，不建议在生产环境中使用）。当访问一个对象的属性或方法时，如果在该对象上找不到，JavaScript 引擎就会沿着这个原型链向上查找，直到找到该属性或方法或者到达原型链的顶端（`Object.prototype`）。

例如：

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

console.log(myDog.isAlive); // true，通过原型链从 Animal 的实例继承而来
myDog.move(); // Moving...，通过原型链从 Animal 的原型对象继承而来
myDog.bark(); // Woof!，直接在 Dog 的原型对象上定义的方法
```

**二、原型链的构成**

1. 当创建一个函数时，JavaScript 会自动为该函数创建一个`prototype`属性，它指向一个原型对象。
2. 当使用这个函数作为构造函数创建对象实例时，这些实例的内部链接`[[Prototype]]`会指向构造函数的原型对象。
3. `Object.prototype`是所有对象的最终原型，它包含一些通用的方法，如`toString`、`valueOf`等。

**三、原型链的作用**

1. **实现继承**：通过原型链，可以让一个对象继承另一个对象的属性和方法，从而实现代码的复用。
2. **动态扩展**：可以在原型对象上添加新的属性和方法，所有的对象实例都可以立即访问到这些新添加的内容。

**四、注意事项**

1. 原型链查找可能会导致性能问题，特别是在原型链较长的情况下，因为每次查找都需要遍历整个原型链。
2. 如果在原型链的不同层次上定义了同名的属性或方法，靠近对象实例的属性或方法会覆盖更上层的同名属性或方法。
