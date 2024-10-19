# 函数没有重写

严格来说，"重写"（Overriding）是面向对象编程中的概念，特指在类的继承关系中，子类**重写**父类的方法以改变其行为。因此，**函数**（function）这个术语本身通常不涉及“重写”的概念，因为函数没有类和继承的关系。然而，如果函数存在于面向对象语言的上下文中（如方法），且有继承关系时，函数也可以被重写。

#### 函数 vs 方法

* **函数**（Function）是独立的代码块，可能没有类的上下文。
* **方法**（Method）是面向对象编程中类的一部分，是函数在类中的表现形式。

由于函数没有继承关系，所以函数不能“重写”。但是在某些语言中，像 C++ 中的全局函数，无法重写，只能重载。

**C 语言中的函数**

在 C 语言中，函数是没有继承关系的，因此没有“重写”这一概念。C 语言只支持函数的**重载**（通过变参、宏等方式实现的类似效果），而不能像面向对象语言那样进行重写。

**面向对象语言中的方法重写**

在面向对象的上下文中，方法是可以被重写的，因为它们属于类，并且类有继承关系。而函数作为面向过程的独立模块，无法参与这种行为。

#### 总结

* **函数**没有“重写”这一概念，因为没有继承关系。
* **方法**（类中的函数）可以在面向对象的语言中进行重写（如 Java、C++、Objective-C 等），前提是它们存在于继承体系中。