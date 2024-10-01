# 基本内容

在 Rust 中，泛型（Generics）是一种强大的特性，允许你在编写函数、结构体、枚举或特征时不指定具体的类型，而是在使用时再确定类型。这种灵活性使得代码更加可重用和类型安全。

#### 1. **Rust 中的泛型内容**

**1.1. 泛型函数**

你可以定义接受任意类型参数的函数。

```rust
fn print_value<T: std::fmt::Debug>(value: T) {
    println!("{:?}", value);
}

fn main() {
    print_value(42); // 整数
    print_value("Hello"); // 字符串
}
```

**1.2. 泛型结构体**

你可以定义使用泛型的结构体。

```rust
struct Pair<T, U> {
    first: T,
    second: U,
}

fn main() {
    let pair = Pair { first: 1, second: "apple" };
    println!("first: {}, second: {}", pair.first, pair.second);
}
```

**1.3. 泛型特征**

特征可以定义泛型，允许类型实现特征的方法。

```rust
trait Summary<T> {
    fn summarize(&self) -> T;
}

struct NewsArticle {
    headline: String,
    content: String,
}

impl Summary<String> for NewsArticle {
    fn summarize(&self) -> String {
        format!("{} - {}", self.headline, self.content)
    }
}
```

#### 2. **与其他语言的泛型比较**

| 特性        | Rust 泛型       | C++ 模板       | Java 泛型      | Swift 泛型     |
| --------- | ------------- | ------------ | ------------ | ------------ |
| **类型安全**  | 编译时类型检查，确保安全  | 编译时生成代码，类型安全 | 编译时类型检查，确保安全 | 编译时类型检查，确保安全 |
| **灵活性**   | 高度灵活，可与特征结合使用 | 高度灵活，支持模板元编程 | 受限于对象类型      | 高度灵活，支持协议    |
| **代码复用**  | 允许多种类型共享代码    | 允许多种类型共享代码   | 允许不同类型共享代码   | 允许不同类型共享代码   |
| **特化支持**  | 不支持类型特化       | 支持模板特化       | 不支持类型特化      | 支持类型约束       |
| **运行时性能** | 无运行时开销        | 编译后直接替换，性能接近 | 可能存在运行时类型擦除  | 无运行时开销       |

#### 3. **总结**

Rust 的泛型提供了类型安全和灵活性，适合构建可重用的代码。与 C++ 的模板相比，Rust 的泛型更易于使用且安全性更高，但不支持复杂的模板元编程。与 Java 和 Swift 的泛型相比，Rust 在性能上没有运行时开销，适合性能要求较高的场景。整体而言，Rust 的泛型系统在编译时提供了强大的类型检查和灵活性。
