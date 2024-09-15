# 变量类型

在 Swift 中，数据类型可以分为 **值类型（Value Types）** 和 **引用类型（Reference Types）**。这两种类型的核心区别在于它们的存储和复制行为。

#### 值类型

值类型在赋值或传递给函数时，会创建其副本（即拷贝），修改副本不会影响原来的值。值类型主要存储在栈（Stack）上，比较轻量，适合处理简单的数据。

Swift 中的常见值类型包括：

1. **基本数据类型（Primitive Types）**：
   * `Int`: 整数类型
   * `Float` 和 `Double`: 浮点数类型
   * `Bool`: 布尔值类型
   * `Character`: 单字符类型
   * `String`: 字符串类型，尽管是复杂类型，但在 Swift 中仍然是值类型
2.  **结构体（Structs）**：

    * Swift 的 `struct` 是典型的值类型。所有使用 `struct` 声明的类型都是值类型。
    * 例如：`Point`, `Size`, `Date` 等。

    示例：

    ```swift
    struct Point {
        var x: Int
        var y: Int
    }

    var point1 = Point(x: 10, y: 20)
    var point2 = point1  // 复制 point1，创建新副本
    point2.x = 30
    // point1.x 仍然为 10，不受 point2 修改的影响
    ```
3. **枚举（Enum）**：
   * 枚举类型也是值类型。每次使用枚举时，都会复制一个新实例。
   * 例如：`enum Direction { case north, south, east, west }`
4. **元组（Tuple）**：
   * 元组也是值类型。它们可以包含多个值，并且每次赋值时会创建副本。
   * 例如：`let coordinates = (x: 10, y: 20)`

#### 引用类型

引用类型的实例在赋值或传递给函数时不会复制，而是传递引用。也就是说，修改引用类型的实例会影响所有持有该实例的引用。引用类型的实例通常存储在堆（Heap）上。

Swift 中的引用类型包括：

1.  **类（Classes）**：

    * 使用 `class` 声明的类型是引用类型。类的实例在赋值时不会被复制，而是传递其引用。
    * 例如：`class Person { var name: String }`

    示例：

    ```swift
    class Person {
        var name: String
        init(name: String) {
            self.name = name
        }
    }

    var person1 = Person(name: "Alice")
    var person2 = person1  // person2 是 person1 的引用
    person2.name = "Bob"
    // person1.name 现在也是 "Bob"
    ```
2. **函数（Functions）**：
   * 函数本质上是引用类型。将函数赋值给变量时，它们的引用被传递，而不是创建新副本。
   * 例如：`let greet = { print("Hello!") }`

#### 值类型与引用类型的区别

* **存储位置**：值类型通常存储在栈上，引用类型存储在堆上。
* **复制行为**：值类型在赋值或传递时会创建副本，引用类型则传递引用。
* **性能差异**：由于值类型通常存储在栈上，操作简单类型时，值类型的性能可能更高，特别是在频繁创建和销毁实例的场景下。

#### 总结

* **Swift 中的值类型** 包括：`Int`, `Float`, `Double`, `Bool`, `String`, `Character`, `Struct`, `Enum`, `Tuple` 等。
* **Swift 中的引用类型** 包括：`Class` 和 `Function`。

这些类型的不同使用场景取决于代码的需求，如果需要避免共享状态，值类型通常是更好的选择；如果需要共享状态或管理复杂对象，引用类型则更合适。
