# 类（对象）

在Scala中，类是构建对象的基本结构，允许你定义属性和方法。以下是一些关键概念和示例：

#### 定义类

1.  **基本类**：

    ```scala
    class Person(val name: String, var age: Int) {
      def greet(): String = s"Hello, my name is $name and I am $age years old."
    }
    ```
2.  **创建对象**：

    ```scala
    val person = new Person("Alice", 30)
    println(person.greet()) // 输出: Hello, my name is Alice and I am 30 years old.
    ```

#### 伴生对象

*   伴生对象用于创建工厂方法或静态方法：

    ```scala
    object Person {
      def apply(name: String, age: Int): Person = new Person(name, age)
    }

    val person2 = Person("Bob", 25) // 使用伴生对象创建实例
    ```

#### 类的继承

*   可以通过扩展类来实现继承：

    ```scala
    class Employee(name: String, age: Int, val salary: Double) extends Person(name, age) {
      def displaySalary(): String = s"My salary is $$salary."
    }

    val employee = new Employee("Charlie", 28, 50000)
    println(employee.greet()) // 输出: Hello, my name is Charlie and I am 28 years old.
    println(employee.displaySalary()) // 输出: My salary is $50000.0.
    ```

#### 抽象类

*   抽象类可以包含未实现的方法，子类必须实现这些方法：

    ```scala
    abstract class Animal {
      def sound(): String // 抽象方法
    }

    class Dog extends Animal {
      def sound(): String = "Woof!"
    }

    val dog = new Dog()
    println(dog.sound()) // 输出: Woof!
    ```

#### 特质（Trait）

*   特质是一种轻量级的抽象类，可以混入其他类：

    ```scala
    trait Speak {
      def speak(): String
    }

    class Cat extends Animal with Speak {
      def sound(): String = "Meow!"
      def speak(): String = "I am a cat."
    }

    val cat = new Cat()
    println(cat.sound()) // 输出: Meow!
    println(cat.speak()) // 输出: I am a cat.
    ```

这些示例展示了Scala中类的基本用法和特性。
