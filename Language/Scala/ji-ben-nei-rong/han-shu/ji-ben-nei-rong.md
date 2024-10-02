# 基本内容

<mark style="color:red;">**函数是一等公民，这意味着函数可以像值一样被传递、赋值和返回**</mark>。Scala支持多种类型的函数，包括普通函数、匿名函数（lambda）和高阶函数。以下是Scala中函数的主要概念和示例：

#### 1. 定义函数

使用`def`关键字定义一个函数。

```scala
def add(x: Int, y: Int): Int = {
  x + y
}

println(add(2, 3)) // 输出: 5
```

#### 2. 匿名函数（Lambda）

可以使用简洁的语法定义匿名函数，通常用于短小的函数。

```scala
val multiply = (x: Int, y: Int) => x * y

println(multiply(3, 4)) // 输出: 12
```

#### 3. 高阶函数

高阶函数是指接受其他函数作为参数或返回函数的函数。

```scala
def applyFunction(f: Int => Int, value: Int): Int = {
  f(value)
}

val double = (x: Int) => x * 2

println(applyFunction(double, 5)) // 输出: 10
```

#### 4. 函数柯里化

函数柯里化是将一个接受多个参数的函数转换为一系列接受单一参数的函数的技术。

```scala
def addCurried(x: Int)(y: Int): Int = x + y

val addTwo = addCurried(2) _ // 记住第一个参数
println(addTwo(3)) // 输出: 5
```

#### 5. 默认参数和命名参数

可以为函数参数提供默认值，并且可以通过命名参数来调用函数。

```scala
def greet(name: String = "World"): String = {
  s"Hello, $name!"
}

println(greet())         // 输出: Hello, World!
println(greet("Alice"))  // 输出: Hello, Alice!
```

#### 6. 变量参数（可变参数）

使用`*`来定义可变参数，允许传入任意数量的参数。

```scala
def sum(numbers: Int*): Int = {
  numbers.sum
}

println(sum(1, 2, 3, 4)) // 输出: 10
```

#### 7. 函数类型

可以定义函数的类型，描述函数的参数类型和返回类型。

```scala
val stringLength: String => Int = (s: String) => s.length
println(stringLength("Hello")) // 输出: 5
```

#### 总结

Scala中的函数提供了强大的功能和灵活性，允许你以多种方式组织和使用代码。
