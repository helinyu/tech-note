---
description: 常见的是针对集合的处理的函数方法
---

# 高阶函数

在 Rust 中，高阶函数是指可以接收其他函数作为参数或返回函数的函数。高阶函数使得函数式编程风格在 Rust 中得以实现，增强了代码的灵活性和可重用性。

#### 定义高阶函数

下面是一个简单的高阶函数示例：

```rust
fn apply<F>(func: F) -> i32 
where 
    F: Fn(i32) -> i32,
{
    func(5)
}

fn main() {
    let double = |x| x * 2; // 定义一个闭包
    let result = apply(double);
    println!("Result: {}", result); // 输出: Result: 10
}
```

#### 特点

1. **闭包支持**：Rust 支持闭包作为参数，这使得高阶函数的定义非常灵活。
2. **函数类型**：可以使用 `Fn`、`FnMut` 和 `FnOnce` 来限制参数类型，这取决于闭包的使用场景。

#### 示例：返回高阶函数

可以定义一个返回高阶函数的函数：

```rust
fn make_adder(x: i32) -> impl Fn(i32) -> i32 {
    move |y| x + y // 返回一个闭包
}

fn main() {
    let add_five = make_adder(5);
    println!("Result: {}", add_five(10)); // 输出: Result: 15
}
```

#### 优势

* **简洁性**：高阶函数能减少代码重复，提高代码的可读性。
* **抽象性**：允许更高层次的抽象，使得程序逻辑更清晰。

#### 总结

Rust 中的高阶函数为编程提供了灵活的方式，使得函数的组合和复用变得简单，是实现函数式编程风格的关键特性之一。通过使用闭包和函数类型，Rust 提供了强大的工具来处理复杂的逻辑和操作。
