# 基本内容

在 Rust 中，控制语句用于控制程序的流向，主要包括条件语句、循环语句和模式匹配。以下是一些常见的控制语句：

#### 1. **条件语句**

**1.1. if 语句**

用于根据条件执行不同的代码块。

```rust
let number = 5;

if number < 10 {
    println!("小于10");
} else if number == 10 {
    println!("等于10");
} else {
    println!("大于10");
}
```

**1.2. match 语句**

用于模式匹配，可以替代复杂的 if-else 结构。

```rust
let number = 3;

match number {
    1 => println!("一"),
    2 => println!("二"),
    3 => println!("三"),
    _ => println!("其他"),
}
```

#### 2. **循环语句**

**2.1. loop**

无限循环，直到显式中断。

```rust
let mut count = 0;

loop {
    count += 1;
    if count >= 5 {
        break; // 中断循环
    }
    println!("当前计数: {}", count);
}
```

**2.2. while**

在条件为真时执行循环。

```rust
let mut count = 0;

while count < 5 {
    println!("当前计数: {}", count);
    count += 1;
}
```

**2.3. for**

用于遍历集合（如数组、切片、范围等）。

```rust
let numbers = [1, 2, 3, 4, 5];

for number in numbers.iter() {
    println!("{}", number);
}

for i in 0..5 { // 0 到 4
    println!("{}", i);
}
```

#### 3. **控制流的关键字**

* **break**：退出循环。
* **continue**：跳过当前循环迭代，进入下一次迭代。
* **return**：从函数中返回值。

#### 4. **总结**

Rust 的控制语句提供了灵活且强大的方式来管理程序流，包括条件分支、循环和模式匹配等。这些控制语句结合 Rust 的类型系统和模式匹配，使得编写逻辑清晰且类型安全的代码变得更加容易。
