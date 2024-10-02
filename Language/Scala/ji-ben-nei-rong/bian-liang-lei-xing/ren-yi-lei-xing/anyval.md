# AnyVal

在 Scala 中，`AnyVal` 是所有值类型的超类型，表示所有非引用类型的基本数据类型。它是 Scala 类型层次结构的一部分，所有值类型都是 `AnyVal` 的子类型。以下是关于 `AnyVal` 的一些关键点：

#### 1. 定义

* `AnyVal` 是 Scala 中的一个类型，用于表示所有基本值类型，如整数、浮点数、字符和布尔值等。

#### 2. 子类型

`AnyVal` 包含以下常见的子类型：

* **整型**：
  * `Byte`
  * `Short`
  * `Int`
  * `Long`
* **浮点型**：
  * `Float`
  * `Double`
* **字符型**：
  * `Char`
* **布尔型**：
  * `Boolean`
* **其他类型**：
  * Scala 还支持一些其他的值类型，如 `Unit` 和 `Null`。

#### 3. 特性

* **不可变性**：`AnyVal` 类型的实例通常是不可变的。修改这些类型的值实际上会创建一个新的实例。
* **性能**：由于 `AnyVal` 类型的值在堆外存储，通常比引用类型更高效。
* **值类型 vs 引用类型**：`AnyVal` 表示值类型，与 `AnyRef`（所有引用类型的超类型）相对。值类型在使用时直接存储数据，而引用类型存储对象的引用。

#### 4. 使用场景

* 使用 `AnyVal` 可以编写可以接受任何基本值类型的方法，或者在需要支持多种数值类型的集合中。

#### 5. 示例

以下是一个使用 `AnyVal` 的示例：

```scala
def add(x: AnyVal, y: AnyVal): AnyVal = (x, y) match {
  case (a: Int, b: Int) => a + b
  case (a: Double, b: Double) => a + b
  case _ => throw new IllegalArgumentException("Unsupported types")
}

val sumInt = add(5, 10)          // 返回 Int
val sumDouble = add(5.5, 2.3)    // 返回 Double
```

#### 6. 小结

* `AnyVal` 是 Scala 中所有值类型的超类型，提供了一种处理基本数据类型的统一方式。
* 使用 `AnyVal` 提供了灵活性，但在实际开发中，推荐使用更具体的类型以提高类型安全性和可读性。
