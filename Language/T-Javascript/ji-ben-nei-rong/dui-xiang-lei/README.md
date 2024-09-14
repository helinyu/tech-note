# 对象（类）

&#x20;在 JavaScript 中，类（class）和对象（object）是面向对象编程的重要概念。

**一、类（class）**

1.  定义：

    * 在 ES6 中引入了`class`关键字来定义类，它提供了一种更接近传统面向对象编程语言的语法来创建对象的模板。
    * 例如：

    ```javascript
    class Person {
      constructor(name, age) {
        this.name = name;
        this.age = age;
      }

      sayHello() {
        console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
      }
    }
    ```
2. 组成部分：
   * **构造函数（constructor）**：用于初始化对象的属性。当使用`new`关键字创建类的实例时，构造函数会被自动调用。
   * **方法**：定义在类中的函数，用于描述对象的行为。
3.  继承：

    * 通过`extends`关键字可以实现类的继承。子类可以继承父类的属性和方法，并可以添加自己的属性和方法或重写父类的方法。
    * 例如：

    ```javascript
    class Student extends Person {
      constructor(name, age, grade) {
        super(name, age);
        this.grade = grade;
      }

      study() {
        console.log(`${this.name} is studying.`);
      }
    }
    ```

**二、对象（object）**

1.  定义：

    * 对象是类的实例化结果，它包含了类中定义的属性和方法的具体值。
    * 例如：

    ```javascript
    const person1 = new Person('Alice', 30);
    const student1 = new Student('Bob', 20, 'A');
    ```
2. 特点：
   * **属性访问**：可以通过点语法（`.propertyName`）或方括号语法（`object['propertyName']`）来访问对象的属性。
   * **方法调用**：可以通过点语法来调用对象的方法。
   * **动态性**：JavaScript 的对象是动态的，可以在运行时添加、修改或删除属性和方法。
3.  创建方式：

    * **使用构造函数**：通过自定义构造函数或内置构造函数（如`Object`、`Array`等）来创建对象。
    * **对象字面量**：使用花括号`{}`来创建一个包含属性和方法的对象。
    * 例如：

    ```javascript
    // 使用构造函数
    function Car(make, model) {
      this.make = make;
      this.model = model;
    }
    const myCar = new Car('Toyota', 'Camry');

    // 对象字面量
    const book = {
      title: 'JavaScript for Beginners',
      author: 'John Doe',
      read: function() {
        console.log(`Reading ${this.title} by ${this.author}.`);
      }
    };
    ```

总之，类是对象的模板，用于定义对象的结构和行为，而对象是类的具体实例，包含了类中定义的属性和方法的实际值。JavaScript 的类和对象提供了一种强大的方式来组织和管理代码，实现面向对象编程的原则，如封装、继承和多态。
