# 内置高阶函数

是的，Rust 标准库中内置了多种高阶函数，特别是在集合类型（如 `Vec`、`Iterator`）上。以下是一些常用的内置高阶函数示例：

#### 1. **Iterator Trait**

`Iterator` trait 提供了许多高阶函数，如 `map`、`filter` 和 `fold`。

**示例**

```rust
fn main() {
    let numbers = vec![1, 2, 3, 4, 5];

    // 使用 map 高阶函数
    let doubled: Vec<i32> = numbers.iter().map(|&x| x * 2).collect();
    println!("{:?}", doubled); // 输出: [2, 4, 6, 8, 10]

    // 使用 filter 高阶函数
    let evens: Vec<i32> = numbers.iter().filter(|&&x| x % 2 == 0).cloned().collect();
    println!("{:?}", evens); // 输出: [2, 4]

    // 使用 fold 高阶函数
    let sum: i32 = numbers.iter().fold(0, |acc, &x| acc + x);
    println!("{}", sum); // 输出: 15
}
```

#### 2. **闭包与高阶函数**

Rust 支持将闭包作为参数传递给其他函数，这本身就是一种高阶函数的使用方式。

**示例**

```rust
fn apply<F>(func: F, value: i32) -> i32 
where 
    F: Fn(i32) -> i32,
{
    func(value)
}

fn main() {
    let square = |x| x * x;
    let result = apply(square, 5);
    println!("{}", result); // 输出: 25
}
```

#### 总结

Rust 内置了许多高阶函数，尤其是在迭代器和集合操作中，通过这些高阶函数，开发者可以以更简洁和声明式的方式处理数据。这些函数使得 Rust 的函数式编程风格更加灵活和强大。
