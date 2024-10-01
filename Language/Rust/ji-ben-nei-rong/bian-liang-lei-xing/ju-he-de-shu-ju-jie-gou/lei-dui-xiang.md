# 类（对象）

面向对象语言来说都是有这个的

```ini
除了c/c++ 这种底层语言有结构体/共用体之外，其他的新语言，都不会有了。

类： 如何定义的，写法， 有类对象这种概念
属性：如何定义属性的，和该语言的变量定义有关。 也可能要区分类属性和对象属性
方法: 可能有对象方法和类方法区分。
继承： 多重继承？
访问权限控制
```

```dockerfile
1、创建对象
2、调用（访问属性和方法）
3、特殊方法：定义描述类的字符串形式
```



<mark style="color:red;">**没有类的概念， 都是通过结构体 + trait来实现的。**</mark>&#x20;

在 Rust 中，并没有直接的 "类" 概念，像在面向对象编程语言（如 C++、Java 或 Swift）中那样使用 `class` 关键字定义类。然而，Rust 提供了类似于类的功能，主要通过 **结构体（structs）** 和 **trait** 来实现封装、继承（行为复用）、以及多态等面向对象的特性。

#### 类的替代者：结构体与 impl 块

Rust 中的类可以用 **结构体（struct）** 来定义数据，并通过 **`impl` 块** 为结构体实现方法，这与面向对象编程中的类非常相似。

**示例：定义类及其方法**

```rust
// 定义一个结构体
struct Rectangle {
    width: u32,
    height: u32,
}

// 使用 impl 块为结构体定义方法
impl Rectangle {
    // 关联函数（类似于静态方法）
    fn new(width: u32, height: u32) -> Rectangle {
        Rectangle { width, height }
    }

    // 普通方法（类似于实例方法）
    fn area(&self) -> u32 {
        self.width * self.height
    }

    fn perimeter(&self) -> u32 {
        2 * (self.width + self.height)
    }
}

fn main() {
    let rect = Rectangle::new(10, 20);  // 创建实例
    println!("Area: {}", rect.area());  // 调用方法
    println!("Perimeter: {}", rect.perimeter());
}
```

在这个例子中，`Rectangle` 结构体相当于类的属性，`impl` 块中的方法相当于类的方法。`self` 相当于面向对象中的 `this` 指针，表示当前实例。

#### 类中的静态方法与实例方法

在 Rust 中，可以在 `impl` 块中定义两类方法：

* **关联函数**（不带 `self` 参数）：相当于类的静态方法。例如，`Rectangle::new()`。
* **实例方法**（带 `&self` 参数）：相当于类的实例方法。例如，`rect.area()`。

#### 多个 `impl` 块

Rust 允许为同一个结构体定义多个 `impl` 块。这在需要分开实现不同功能时非常有用。

**示例：**

```rust
struct Circle {
    radius: f64,
}

impl Circle {
    fn new(radius: f64) -> Circle {
        Circle { radius }
    }
    
    fn area(&self) -> f64 {
        3.14 * self.radius * self.radius
    }
}

impl Circle {
    fn circumference(&self) -> f64 {
        2.0 * 3.14 * self.radius
    }
}
```

#### 类的继承与多态：Trait 和 Trait 对象

Rust 没有直接的类继承机制，但通过 **trait**（特性）可以实现行为的复用和多态。`trait` 类似于接口或抽象类，它定义了一组方法，而结构体可以实现这些 trait，从而获得这些方法的行为。

**示例：实现类似于继承的行为**

```rust
// 定义 Trait，相当于接口
trait Shape {
    fn area(&self) -> f64;
    fn perimeter(&self) -> f64;
}

// 实现 Trait
struct Rectangle {
    width: f64,
    height: f64,
}

impl Shape for Rectangle {
    fn area(&self) -> f64 {
        self.width * self.height
    }
    
    fn perimeter(&self) -> f64 {
        2.0 * (self.width + self.height)
    }
}

struct Circle {
    radius: f64,
}

impl Shape for Circle {
    fn area(&self) -> f64 {
        3.14 * self.radius * self.radius
    }
    
    fn perimeter(&self) -> f64 {
        2.0 * 3.14 * self.radius
    }
}

fn print_shape_info(shape: &dyn Shape) {
    println!("Area: {}", shape.area());
    println!("Perimeter: {}", shape.perimeter());
}

fn main() {
    let rect = Rectangle { width: 10.0, height: 20.0 };
    let circle = Circle { radius: 5.0 };

    print_shape_info(&rect);
    print_shape_info(&circle);
}
```

这里，`Shape` 是一个 trait，定义了 `area` 和 `perimeter` 方法，而 `Rectangle` 和 `Circle` 通过实现这个 trait 来具备这些方法。通过传入 `&dyn Shape`，实现了类似于多态的行为。

#### 面向对象的三大特性在 Rust 中的表现

1.  **封装**：通过结构体和 `impl` 实现封装，结构体中的字段默认是私有的，只能通过公有方法访问（通过 `pub` 关键字可以公开字段和方法）。

    ```rust
    struct Person {
        name: String,
        age: u32,
    }

    impl Person {
        pub fn new(name: String, age: u32) -> Person {
            Person { name, age }
        }

        pub fn get_age(&self) -> u32 {
            self.age
        }
    }
    ```
2. **继承**：Rust 没有传统的继承机制，但可以通过 trait 来复用行为。
3. **多态**：Rust 使用 trait 和 trait 对象来实现动态分发，从而提供类似于面向对象的多态机制。

#### Rust 与其他语言中类的区别

* **没有继承**：Rust 没有类的继承，而是通过 trait 系统实现行为复用。这样可以避免多重继承带来的复杂性，同时使得代码更加模块化和灵活。
* **默认不可变性**：Rust 中的结构体字段和方法默认是不可变的（除非使用 `mut` 关键字）。这一点与像 C++ 或 Java 这样的语言有所不同，在这些语言中，类的字段和方法默认是可变的。
* **更强的安全性**：Rust 强调内存安全，因此编译时会对引用、生命周期、所有权进行严格检查，确保不存在数据竞争、悬空指针等问题。
* **组合优于继承**：Rust 鼓励使用 **组合**（composition）而非继承。通过将结构体作为字段嵌套在其他结构体中，Rust 实现了类的一些组合特性。

#### 总结

虽然 Rust 不提供传统的类和继承机制，但它通过 **结构体** 和 **trait** 实现了类似的面向对象编程功能，包括封装、多态和行为复用。Rust 通过这些设计，确保了更好的内存安全性和更清晰的代码结构，避免了继承带来的复杂性和潜在问题。
